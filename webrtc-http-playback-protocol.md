---
docname: 
title: WebRTC HTTP Playback Protocol (WHPP)
abbrev: 
category: 
ipr: 
area: 
workgroup: 

keyword: WebRTC

stand_alone: yes
pi: [toc, sortrefs, symrefs]

author:
-
    ins: M. Spangenberg
    name: Marcus Spangenberg
    organization: Eyevinn Technology
    email: marcus.spangenberg@eyevinn.se
-
    ins: J. Birme
    name: Jonas Birme
    organization: Eyevinn Technology
    email: jonas.birme@eyevinn.se

normative:
  RFC2119:
  draft-ietf-wish-whip-02:

--- abstract

--- middle

# Introduction

As interest in WebRTC based media streaming for non-conferencing scenarios such as broadcast is increasing, there is a need for standardizing some aspects of RTC session setup and signalling specifically for those scenarios. Since the mechanism to exchange SDP offers and answers during session setup is not part of the WebRTC standard there is no common way of interacting with media servers for ingesting and playing back WebRTC based media streams for broadcast scenarios. 

On the stream ingestion side, there is ongoing work in defining a standard in {{!draft-ietf-wish-whip-02}}. This document focuses on the playback side, and proposes an HTTP based protocol for negotiating a playback client viewer session for consuming WebRTC based broadcast streams. This document also adds some constraints to how WebRTC is to be used in order to simplify operation.

# Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in {{!RFC2119}}.

- Playback client: WebRTC broadcast media stream consumer.
- Playback endpoint: Playback server receiving the initial HTTP request.
- Playback channel URL: URL on the playback endpoint referring to a specific media stream broadcast channel.
- Viewer resource: Allocated resource on the playback endpoint for an ongoing viewer session allocated by a playback client.
- Media Server: A WebRTC media server sending media streams consumed by the playback client.

# Overview

Playback of a specific media broadcast channel is started by a playback client by sending an HTTP POST request to a playback channel URL, creating a viewer resource on the specified channel. The playback endpoint responds with a viewer resource URL and the initial SDP offer used for session negotiation. Since the playback client assumes the role of SDP answerer in this protocol, it is responsible for negotiating an SDP answer and sending it back to the viewer resource URL as an HTTP PUT request.

# Protocol Operation

The playback client connects to a channel by creating a viewer resource on the channel endpoint. The viewer resource is created by sending an HTTP POST request to the channel endpoint. The payload SHOULD be an empty JSON object. If successful, the channel endpoint MUST respond with HTTP status code 201 (created) and a JSON payload containing the initial SDP offer and additional metadata about the media streams contained in that offer. The response SHALL also contain a Location header containing the viewer resource URL.

~~~
Request

POST /channel/<channelId>
Content-type: application/json
Body:
{}

Response

Status: 201
Location: Resource URL
Content-type: application/whpp+json
Body:
{
   "offer": "...",
   "mediaStreams": [
      {"msid", "senderId"}
   ]
}
~~~

To complete the connection, the playback client SHALL send an SDP answer as an HTTP PUT request to the viewer resource URL. If successful, the viewer resource MUST respond with HTTP status code 204 (no content).

~~~
Request

PUT /channel/<channelId>/<viewerId>
Content-type: application/whpp+json
Body:
{
   "answer": "..."
}

Response

Status: 204
~~~

Additionally, the playback client MAY use trickle-ICE. If it is to be used, the playback client MAY send newly gathered ICE candidates to the viewer resource URL as HTTP PATCH requests. The request payload SHALL contain a single ICE candidate. If successful, the viewer resource SHALL respond with HTTP status 204 (no content). The viewer resource MAY support only ICE lite in which case it MUST respond with HTTP status code 405 (method not allowed).

~~~
Request

PATCH /channel/<channelId>/<viewerId>
Content-type: application/whpp+json
Body:
{
   "candidate": "..."
}

Response

Status: 204
~~~

# Security Considerations

# IANA Considerations

# Acknowledgements

--- back
