link: https://tailscale.com/blog/how-nat-traversal-works/
name:
topic:
author:
tags:
#todo
# How NAT traversal works

establishing a peer-to-peer connection between two machines.

Let’s say you’re making your own protocol and that you want NAT traversal. You need two things.

First, the protocol should be based on UDP. You _can_ do NAT traversal with TCP, but it adds another layer of complexity to an already quite complex problem, and may even require kernel customizations depending on how deep you want to go. We’re going to focus on UDP for the rest of this article.

If you’re reaching for TCP because you want a stream-oriented connection when the NAT traversal is done, consider using QUIC instead. It builds on top of UDP, so we can focus on UDP for NAT traversal and still have a nice stream protocol at the end.

Second, you need direct control over the network socket that’s sending and receiving network packets. As a rule, you can’t take an existing network library and make it traverse NATs, because you have to send and receive extra packets that aren’t part of the “main” protocol you’re trying to speak. Some protocols tightly integrate the NAT traversal with the rest (e.g. WebRTC). But if you’re building your own, it’s helpful to think of NAT traversal as a separate entity that shares a socket with your main protocol. Both run in parallel, one enabling the other.

