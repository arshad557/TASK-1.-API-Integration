# TASK-1.-API-Integration
CODETECH Internship 

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: #f0f8ff;
    }
    .container {
      text-align: center;
      background: white;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      max-width: 400px;
      width: 100%;
    }
    .container h1 {
      margin-bottom: 20px;
    }
    .weather-info {
      margin-top: 20px;
    }
    .loading {
      font-style: italic;
      color: #666;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Weather Information</h1>
    <input type="text" id="city" placeholder="Enter city name" />
    <button id="fetchWeather">Get Weather</button>
    <div class="weather-info" id="weatherInfo">
      <p class="loading" id="loadingMessage">Enter a city to fetch weather data.</p>
    </div>
  </div>

  <script>
    const apiKey = 'your_openweather_api_key'; // Replace with your API key from OpenWeather
    const fetchWeatherButton = document.getElementById('fetchWeather');
    const cityInput = document.getElementById('city');
    const weatherInfoDiv = document.getElementById('weatherInfo');
    const loadingMessage = document.getElementById('loadingMessage');

    fetchWeatherButton.addEventListener('click', () => {
      const city = cityInput.value;

      if (!city) {
        alert('Please enter a city name!');
        return;
      }

      loadingMessage.textContent = 'Fetching weather data...';
      weatherInfoDiv.innerHTML = '';

      fetch(`https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`)
        .then((response) => {
          if (!response.ok) {
            throw new Error('City not found');
          }
          return response.json();
        })
        .then((data) => {
          const { main, weather, name } = data;
          weatherInfoDiv.innerHTML = `
            <h2>${name}</h2>
            <p><strong>Temperature:</strong> ${main.temp} °C</p>
            <p><strong>Condition:</strong> ${weather[0].description}</p>
          `;
        })
        .catch((error) => {
          weatherInfoDiv.innerHTML = `<p style="color: red;">Error: ${error.message}</p>`;
        });
    });
  </script>
</body>
</html>

