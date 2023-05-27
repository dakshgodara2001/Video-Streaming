# Video-Streaming

This is a real-time video chat application using Django, Django Channels, and WebRTC. The application leverages the power of Django Channels to handle WebSocket connections and manage real-time communication, along with WebRTC for peer-to-peer video and audio communication in the browser.

![Screen Shot 2023-05-27 at 10 30 16 PM](https://github.com/dakshgodara2001/Video-Streaming/assets/52131905/a96bfa5e-a328-4380-a073-e354900e41a8)
![Screen Shot 2023-05-27 at 10 31 02 PM](https://github.com/dakshgodara2001/Video-Streaming/assets/52131905/75770d3c-5abe-4309-a84e-628ce52dda5c)


## Features

- Real-time video chat using WebRTC
- Signaling server using Django Channels and WebSockets

## How It Works

This application utilizes the **Session Description Protocol (SDP)** and **WebSocket** for real-time video and audio communication. Here's a basic breakdown of how it works:

### SDP (Session Description Protocol)

SDP is a format for describing networked multimedia sessions, which allows participants to agree on a set of compatible media types. This protocol shares crucial information about a peer that the other peer needs to establish a peer-to-peer (p2p) connection.

### Signaling

Signaling is the process of coordinating communication in order to establish a call. In this application, the Django server acts as the signaling server. Both peers connect to the signaling server using WebSocket. After SDPs are exchanged from both sides, a p2p connection can be established. The signaling server is not required afterwards.

### Groups (Django Channels)

Groups function like chat rooms. They keep track of channel names and allow messages to be sent through all channels in the group to their respective peers.

### Peer Connection Process

Here's how peers connect to each other:

1. A peer joins the room.
2. The peer sends a message to all other peers indicating its entry. All other peers get notified of the new peer through this message.
3. Each existing peer initiates a peer connection with the new peer by offering an SDP.
4. The new peer receives each offer SDP.
5. The new peer sends a response (an answer SDP) for each offer SDP.
6. Other peers receive their respective answer SDPs.
7. The new peer is now connected with each existing peer, creating a mesh network.

This application uses a mesh network structure, meaning each peer is directly connected to every other peer. This structure is effective for smaller networks but can be bandwidth-intensive as the number of peers increases. For larger networks, consider using a different network structure, such as a star network or a MCU/SFU based architecture.

