# Frequently Asked Questions

## How does the server get prepared for capping a live stream?

We will simply run a browser simulator in the backend and keep recording network traffic. Upon receiving CAP requests, video and chats data will be collected from browser memory.

## Stream Capping Status "not_available"

There may be many reasons why capping resources are not ready, including:

- We do not have enough resources to run browser simulators in the backend
- The browser simulator is starting but not ready yet
- Dawei spilt some coffee into the machine
- Too much smog in Beijing

We are constantly monitoring on number of simulators needed. We will prepare more resources accordingly.
