# webrtc-http-playback-protocol

As interest in WebRTC based media streaming for non-conferencing scenarios such as broadcast is increasing, there is a need for standardizing some aspects of RTC session setup and signalling specifically for those scenarios. Since the mechanism to exchange SDP offers and answers during session setup is not part of the WebRTC standard there is no common way of interacting with media servers for ingesting and playing back WebRTC based media streams for broadcast scenarios.

On the stream ingestion side, there is ongoing work in defining a standard in {{!draft-ietf-wish-whip-02}}. This document focuses on the playback side, and proposes an HTTP based protocol for negotiating a playback client viewer session for consuming WebRTC based broadcast streams. This document also adds some constraints to how WebRTC is to be used in order to simplify operation.

[webrtc-http-playback-protocol.md](https://github.com/Eyevinn/webrtc-http-playback-protocol/blob/master/webrtc-http-playback-protocol.md)

## WHPP Reference Streams

- Sunny Stockholm: https://wrtc-edge.lab.sto.eyevinn.technology:8443/whpp/channel/sthlm

## WHPP Tools and Libraries

- [@eyevinn/whpp-client](https://www.npmjs.com/package/@eyevinn/whpp-client): A Node / JS Library for WHPP.
- [@eyevinn/webrtc-player](https://www.npmjs.com/package/@eyevinn/webrtc-player): Media Server Independent WebRTC Player with WHPP support included. Demo available [here](https://webrtc.player.eyevinn.technology).
- [@eyevinn/wrtc-egress](https://www.npmjs.com/package/@eyevinn/wrtc-egress): Standardized WebRTC Egress Endpoint Library with WHPP support.
- [Eyevinn Web Player](https://web.player.eyevinn.technology): Open source HTML video player with support for HLS, MPEG-DASH and WHPP.

## Docker Container Images:

- [eyevinntechnology/wrtc-whpp](https://github.com/Eyevinn/docker-wrtc-whpp): WHPP Endpoint
- [eyevinntechnology/wrtc-origin](https://github.com/Eyevinn/docker-wrtc-origin): WHIP Endpoint
- [eyevinntechnology/wrtc-sfu](https://github.com/Eyevinn/docker-wrtc-sfu): Symphony Media Bridge media server

## Reading

- [WebRTC HTTP Playback Protocol (WHPP)](https://dev.to/video/webrtc-http-playback-protocol-whpp-p66)
- [How to setup a lab environment for WebRTC broadcast streaming](https://dev.to/video/how-to-setup-a-lab-environment-for-webrtc-broadcast-streaming-269)
- [WebRTC based distribution with WHIP and WHPP running on AWS Fargate](https://eyevinntechnology.medium.com/webrtc-based-distribution-with-whip-and-whpp-running-on-aws-fargate-b217e4c6e00)
- [WHIP & WHPP for WebRTC based broadcast streaming](https://eyevinntechnology.medium.com/whip-whpp-for-webrtc-based-broadcast-streaming-2cf469e95299)