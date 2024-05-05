# Weather-App
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Weather App</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: linear-gradient(to bottom right, #0080ff, #00ccff);
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
  }
  .container {
    background: rgba(255, 255, 255, 0.8);
    border-radius: 10px;
    padding: 20px;
    text-align: center;
  }
  h1 {
    color: #333;
  }
  #weather {
    margin-top: 20px;
  }
</style>
</head>
<body>
<div class="container">
  <h1>Weather App</h1>
  <div id="weather"></div>
</div>
<script>
  window.addEventListener('load', () => {
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(position => {
        const { latitude, longitude } = position.coords;
        const apiKey = 'YOUR_API_KEY';
        const apiUrl = `https://api.openweathermap.org/data/2.5/weather?lat=${latitude}&lon=${longitude}&appid=${apiKey}&units=metric`;
        
        fetch(apiUrl)
          .then(response => response.json())
          .then(data => {
            const weatherContainer = document.getElementById('weather');
            const temperature = data.main.temp;
            const description = data.weather[0].description;
            const city = data.name;
            
            weatherContainer.innerHTML = `
              <p>Current weather in ${city}: ${description}, ${temperature}°C</p>
            `;
          })
          .catch(error => {
            console.error('Error fetching weather data:', error);
          });
      });
    } else {
      console.error('Geolocation is not supported by this browser.');
    }
  });
</script>
</body>
</html>
