[weather.js](https://github.com/user-attachments/files/23281096/weather.js)[weather.html](https://github.com/user-attachments/files/23281095/weather.html)# WEATHER-REPORT
A SITE TO CHECK THE WEATHER OF UR SPECIFIC ENVIRONMENT
[[redirects]]
from = "/*"
to = "/weather.html"
status = 200[weather.css](https://github.com/user-attachments/files/23281092/weather.css)
body{
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    background-color: rgb(32, 134, 134);
    margin: 0;[Upload// Weather App

const weatherform = document.querySelector(".weatherform");
const cityIn = document.querySelector(".cityIn");
const card = document.querySelector(".card");
const apiKey = "d557621cfbfea2070560eb39c0e1d1cc";

weatherform.addEventListener("submit", async event => {
    event.preventDefault();

    const city = cityIn.value;
    if(city){
        try{
            const weatherData = await getWeatherDet(city);
            displayWeatherInfo(weatherData);
        }
        catch(error){
            console.log(error);
            displayError(error.message);

        }
    }
    else{
        displayError("Please enter a city name");
    }
});

async function getWeatherDet(city) {
    const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;
    const response = await fetch(apiUrl);
    if(!response.ok){
        throw new Error("City not found");
    }
    const data = await response.json();
    return data;
}
function displayWeatherInfo(data) {
    const {name: city,
         main: {temp, humidity},
          weather: [{description, id}]} = data;

    card.textContent = "";
    card.style.display = "flex";

    const cityDisplay = document.createElement("h1");
    cityDisplay.classList.add("cityDisplay");
    cityDisplay.textContent = city;
    card.appendChild(cityDisplay);

    const weatherEmoji = document.createElement("p");
    weatherEmoji.classList.add("weatherEmo");
    weatherEmoji.textContent = getWeatherEmoji(id);
    card.appendChild(weatherEmoji);

    const tempDisplay = document.createElement("p");
    tempDisplay.classList.add("tempDisplay");
    tempDisplay.textContent = `${Math.round(temp)}°C`;
    card.appendChild(tempDisplay);

    const descriptionDisplay = document.createElement("p");
    descriptionDisplay.classList.add("desDisplay");
    descriptionDisplay.textContent = description.charAt(0).toUpperCase() + description.slice(1);
    card.appendChild(descriptionDisplay);

    const humidityDisplay = document.createElement("p");
    humidityDisplay.classList.add("humidityDisplay");
    humidityDisplay.textContent = `Humidity: ${humidity}%`;
    card.appendChild(humidityDisplay);
}
function getWeatherEmoji(weatherId) {
    if(weatherId >= 200 && weatherId < 300){
        return "⛈️"; // Thunderstorm
    }
    else if(weatherId >= 300 && weatherId < 500){
        return "🌧️"; // Drizzle
    }
    else if(weatherId >= 500 && weatherId < 600){
        return "🌦️"; // Rain
    }   
    else if(weatherId >= 600 && weatherId < 700){
        return "❄️"; // Snow
    }
    else if(weatherId >= 700 && weatherId < 800){
        return "🌫️"; // Atmosphere (fog, mist, etc)
    }
    else if(weatherId === 800){    
        return "☀️"; // Clear sky
    }
    else if(weatherId > 800 && weatherId < 900){
        return "🌥️"; // Clouds
    }
    else{
        return "🌪️"; // Unknown condition
    }
}

function displayError(message) {
    card.textContent = "";
    card.style.display = "flex";

    const errorDisplay = document.createElement("p");
    errorDisplay.textContent = message;
    card.appendChild(errorDisplay);
}
ing weather.js…]()

    display: flex;
    flex-direction: column;[<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>weather</title>
    <link rel="stylesheet" href="weather.css">
</head>
<body>
    
    <form class="weatherform">
        <input type="text" class="cityIn" placeholder="Enter city name">
        <button type="submit">Get Weather </button>
    </form>

    <div class="card" style="display: none;">
       
    </div>


    <script src="weather.js"></script>
</body>
</html>Uploading weather.html…]()

    align-items: center;
    
}
.weatherform{
    margin: 25px;

}
.cityIn{
    padding: 10px;
    font-size: 2.1rem;
    font-weight: bold;
    border: 2px solid black;
    border-radius: 20px;
    margin: 10px;
    width: 300px;

}
button[type="submit"]{
    padding: 10px 20px;
    font-weight: bold;
    font-size: 1rem;
    background-color: rgb(188, 0, 0);
    color: white; 
    border: none;
    border-radius: 10px;
    cursor: pointer;   
}

button[type="submit"]:hover{
    background-color: rgb(97, 245, 5);
}
.card{
    background: linear-gradient(190deg, blue, rgb(5, 208, 5));
    box-shadow: 2px 2px 5px rgb(98, 45, 45);
    min-width: 300px;
    display: flex;
    flex-direction: column;
    align-items: center;
    border-radius: 10px;

}
h1{
    font-size: 3rem;
    margin-top: 20px;
    margin-bottom: 20px;
}
p{
    font-size: 1rem;
    margin: 8px 0;

}
.cityDisplay, .tempDisplay{
    font-size: 3rem;
    font-weight: 700;
    color: blanchedalmond;
    margin-bottom: 25px;

}
.humidityDisplay{
    font-weight: 700;
    margin-bottom: 25px;
    font-size: 1.3rem;
}
.desDisplay{
    font-style: italic;
    font-w[weather_fixed.js](https://github.com/user-attachments/files/23281099/weather_fixed.js)
eight: 600;
    font-size: 1rem;
}
.weatherEmo{
    margin: 0;
    font-size: 7rem;
}
.errorDisplay{
    font-size: 1rem;
    font-weight: 700;
    color: azure;
}
