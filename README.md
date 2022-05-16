# webrtc-http-playback-protocol

As interest in WebRTC based media streaming for non-conferencing scenarios such as broadcast is increasing, there is a need for standardizing some aspects of RTC session setup and signalling specifically for those scenarios. Since the mechanism to exchange SDP offers and answers during session setup is not part of the WebRTC standard there is no common way of interacting with media servers for ingesting and playing back WebRTC based media streams for broadcast scenarios.

On the stream ingestion side, there is ongoing work in defining a standard in {{!draft-ietf-wish-whip-02}}. This document focuses on the playback side, and proposes an HTTP based protocol for negotiating a playback client viewer session for consuming WebRTC based broadcast streams. This document also adds some constraints to how WebRTC is to be used in order to simplify operation.

[webrtc-http-playback-protocol.md](https://github.com/Eyevinn/webrtc-http-playback-protocol/blob/master/webrtc-http-playback-protocol.md)
