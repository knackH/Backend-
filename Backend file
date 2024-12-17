const express = require('express');
const cors = require('cors');
const app = express();

app.use(cors()); // Enable CORS
app.use(express.json()); // Parse JSON data from requests

// Temporary in-memory storage for location data
const locationData = [];

// Route to receive latitude and longitude
app.post('/send-location', (req, res) => {
    const { latitude, longitude } = req.body;

    if (latitude && longitude) {
        // Store the location data with a timestamp
        locationData.push({
            latitude,
            longitude,
            timestamp: new Date().toISOString()
        });
        return res.status(200).json({ message: 'Location data received successfully' });
    } else {
        return res.status(400).json({ error: 'Latitude and Longitude are required' });
    }
});

// Admin route to display collected location data
app.get('/admin', (req, res) => {
    // Send all collected location data
    res.json({
        message: 'Collected Location Data',
        data: locationData
    });
});

// Default route for testing
app.get('/', (req, res) => {
    res.send('Server is running. Use /send-location to POST data and /admin to GET data.');
});

// Start the server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
