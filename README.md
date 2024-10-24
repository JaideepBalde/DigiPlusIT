# digiplus-exam
this is my test code
const express = require('express');
const http = require('http');
const socketIo = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = socketIo(server);

let nodes = [
    { id: 1, trafficLoad: 0, linkLoad: 0, packetsInQueue: 0 },
    { id: 2, trafficLoad: 0, linkLoad: 0, packetsInQueue: 0 },
    // Add more nodes as required
];

// Simulate traffic load
function simulateTraffic() {
    nodes.forEach(node => {
        node.trafficLoad = Math.floor(Math.random() * 100);  // Random traffic generation
        node.linkLoad = Math.floor(Math.random() * 100);     // Random link load
        node.packetsInQueue = Math.floor(Math.random() * 20); // Random packets in queue
    });

    io.emit('networkUpdate', nodes);
}

// Send updates every 1 second
setInterval(simulateTraffic, 1000);

// Serve static frontend files
app.use(express.static('public'));

server.listen(3000, () => {
    console.log('Server is running on port 3000');
});
