npm init -y
npm install express axios
const express = require('express');
const axios = require('axios');

const app = express();
const port = 3000; // You can choose any port you like

const apiKey = 'YOUR_WEATHERSTACK_API_KEY'; // Replace with your API key

app.get('/', (req, res) => {
  const city = req.query.city;

  if (!city) {
    return res.send('Please provide a city name.');
  }

  const apiUrl = `http://api.weatherstack.com/current?access_key=<span class="math-inline">\{apiKey\}&query\=</span>{city}`;

  axios.get(apiUrl)
    .then(response => {
      const weatherData = response.data;
      res.json(weatherData);
    })
    .catch(error => {
      console.error('Error fetching weather data:', error);
      res.status(500).send('Error fetching weather data.');
    });
});

app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});


node index.js
