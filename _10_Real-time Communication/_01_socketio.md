# _01_ Socket.io

Socket.IO is a library that enables low-latency, bidirectional and event-based communication between a client and a server.

## 🚀 Why use Socket.io?
- **Reliability:** Falls back to HTTP long-polling if WebSockets aren't available.
- **Auto-reconnect:** Automatically handles connection drops.
- **Namespaces & Rooms:** Built-in logic for segmenting users into different communication channels.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install socket.io express
```

### Step 2: Server Initialization
Attach Socket.io to an HTTP server.

## 💻 Code Sample

```javascript
const express = require('express');
const http = require('http');
const { Server } = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = new Server(server, {
  cors: { origin: "*" }
});

// 1. Connection Event
io.on('connection', (socket) => {
  console.log('⚡ A user connected:', socket.id);

  // 2. Joining a Room
  socket.on('join_room', (room) => {
    socket.join(room);
    console.log(`👤 User joined room: ${room}`);
  });

  // 3. Sending/Receiving Messages
  socket.on('send_message', (data) => {
    // Broadcast to everyone in the room
    io.to(data.room).emit('receive_message', data);
  });

  socket.on('disconnect', () => {
    console.log('🔥 User disconnected');
  });
});

server.listen(3000, () => console.log('🚀 Real-time server on port 3000'));
```
