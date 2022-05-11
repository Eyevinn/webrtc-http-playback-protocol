# Introduction


# Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in {{!RFC2119}}.

- Channel endpoint
- Playback client
- Viewer resource URL
- Media Server

# Overview

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
Content-type: application/json
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
Content-type: application/json
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
{
   "candidate": "..."
}

Response

Status: 204
~~~
