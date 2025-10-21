# Realtime Chat Application

### [Live Site](https://realtime-chat-application.netlify.com)

![Chat Application](https://i.ytimg.com/vi/ZwFA3YMfkoc/maxresdefault.jpg)


Setup:
- run ```npm i && npm start``` for both client and server side to start the development server

## About / Tech details

This project is a realtime chat application built with:
- Frontend: React (single-page app) using socket.io-client to connect to the server.
- Backend: Node.js + Express, using socket.io to manage realtime communication.
- Communication: Rooms-based messaging via Socket.io (join rooms, broadcast to room, emit room data).

How it works (high level)
- Client connects to the server using socket.io and emits a `join` event with { name, room }.
- Server stores the user (in-memory user helper in server/users.js), joins the socket to the room, and emits a welcome `message` to the user and a broadcast `message` to other users in the room.
- When a client sends `sendMessage`, the server retrieves the user and emits a `message` to everyone in the room.
- On disconnect the server removes the user and updates the room via `roomData`.

Common socket events
- join — { name, room } (client -> server)
- message — { user, text } (server -> client)
- sendMessage — message string (client -> server)
- roomData — { room, users } (server -> client)
- disconnect — handled by server when socket disconnects

Quick local run (typical)
1. Open two terminals.
2. Start the server:
   - cd server
   - npm install
   - npm start
3. Start the client:
   - cd client
   - npm install
   - npm start
4. If the server requires environment variables, create a `.env` or copy from `.env.example` and set needed keys (PORT, API_URL, DB_URI, etc.).

Developer notes & suggestions
- Check server/index.js for the exact event names and port (default 5000).
- Verify CORS/origin settings if client and server run on different origins.
- Currently users may be kept in memory — consider persisting messages to a database if persistence is required.
- Add .env.example documenting required environment variables and a top-level script (using concurrently) to start both client and server in one command for convenience.

