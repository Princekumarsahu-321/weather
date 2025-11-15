this is my project
HTML code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Weather App</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

<div class="box">
    <h2>Weather App</h2>

    <input type="text" id="city" placeholder="Enter City">
    <button onclick="getWeather()">Search</button>

    <div id="result"></div>
</div>

<script src="script.js"></script>
</body>
</html>

CSS code

body {
    background: #89cff0;
    font-family: Arial;
}

.box {
    width: 300px;
    margin: 70px auto;
    text-align: center;
    padding: 20px;
    background: white;
    border-radius: 10px;
}

input {
    width: 80%;
    padding: 8px;
    margin-top: 15px;
}

button {
    padding: 8px 20px;
    margin-top: 10px;
    background: #287bff;
    border: none;
    color: white;
    cursor: pointer;
}

body {
    background: #6ec6ff;
    font-family: Arial;
}

.box {
    width: 300px;
    margin: 80px auto;
    text-align: center;
    padding: 20px;
    background: white;
    border-radius: 10px;
    box-shadow: 0 0 10px #0003;
}

input {
    width: 80%;
    padding: 8px;
    margin-top: 10px;
}

button {
    padding: 8px 20px;
    margin-top: 10px;
    background: #287bff;
    border: none;
    color: white;
    cursor: pointer;
    border-radius: 5px;
}

#result {
    margin-top: 20px;
    font-size: 18px;
}

JS code

async function getWeather() {
    let city = document.getElementById("city").value;

    // STEP 1 → City name se latitude & longitude find karo
    let geoURL = `https://geocoding-api.open-meteo.com/v1/search?name=${city}`;

    let geoRes = await fetch(geoURL);
    let geoData = await geoRes.json();

    if (!geoData.results) {
        document.getElementById("result").innerHTML = "City not found!";
        return;
    }

    let lat = geoData.results[0].latitude;
    let lon = geoData.results[0].longitude;
    let cityName = geoData.results[0].name;

    // STEP 2 → Weather data laao (NO API KEY NEEDED)
    let weatherURL =
        `https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current_weather=true`;

    let weatherRes = await fetch(weatherURL);
    let weatherData = await weatherRes.json();

    let temp = weatherData.current_weather.temperature;
    let wind = weatherData.current_weather.windspeed;

    document.getElementById("result").innerHTML = `
        <p><strong>${cityName}</strong></p>
        <p>Temperature: ${temp}°C</p>
        <p>Wind Speed: ${wind} km/h</p>
    `;
}


