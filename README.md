<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            text-align: center;
        }
        h1 {
            margin-top: 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Weather App</h1>
        <div id="weather"></div>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function() {
            const apiKey = 'YOUR_API_KEY'; // Replace 'YOUR_API_KEY' with your actual API key
            const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=New York&appid=${apiKey}&units=metric`;

            fetch(apiUrl)
                .then(response => response.json())
                .then(data => {
                    const weatherData = {
                        temperature: data.main.temp,
                        description: data.weather[0].description,
                        icon: data.weather[0].icon
                    };

                    displayWeather(weatherData);
                })
                .catch(error => console.log(error));

            function displayWeather(data) {
                const weatherDiv = document.getElementById('weather');

                const temperature = data.temperature;
                const description = data.description;
                const iconUrl = `http://openweathermap.org/img/w/${data.icon}.png`;

                const weatherHTML = `
                    <img src="${iconUrl}" alt="${description}">
                    <p>Temperature: ${temperature}°C</p>
                    <p>Description: ${description}</p>
                `;

                weatherDiv.innerHTML = weatherHTML;
            }
        });
    </script>
</body>
</html>
