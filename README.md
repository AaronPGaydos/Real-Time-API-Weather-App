# Weather App

A simple weather app that fetches live weather data using the [OpenWeather API](https://openweathermap.org/).

# Project Structure

weather-app/
│── index.html

│── style.css

│── images/

│   ├── search.png

│   ├── rain.png

│   ├── humidity.png

│   ├── wind.png

│   ├── clouds.png

│   ├── clear.png

│   ├── drizzle.png

│   └── mist.png

│── README.md


## 🚀 Features
- Search for a city and get real-time weather.
- Displays temperature, humidity, and wind speed.
- Dynamic weather icons for different conditions.
- Error handling for invalid city names.

## ⚙️ Setup

Clone this repository:

git clone https://github.com/aaronpgaydos/Real-Time-API-Weather-App.git
cd Real-Time-API-Weather-App


Open index.html in your browser.

Replace "YOUR_API_KEY" with your own OpenWeather API key.

Add images inside the /images folder.

---

## 📂 Project Files

### `index.html`
```html
<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

<div class="card">
    <div class="search">
        <input type="text" placeholder="enter city name" spellcheck="false">
        <button><img src="images/search.png"></button>
    </div>
    <div class="error">
        <p>Invalid city name</p>
    </div>
    <div class="weather">
        <img src="images/rain.png" class="weather-icon">
        <h1 class="temp">72°F</h1>
        <h2 class="city">New York</h2>
        <div class="details">
            <div class="col">
                <img src="images/humidity.png">
                <div>
                    <p class="humidity">50%</p>
                    <p>Humidity</p>
                </div>
            </div>
            <div class="col">
                <img src="images/wind.png">
                <div>
                    <p class="wind">10 mp/h</p>
                    <p>Wind Speed</p>
                </div>
            </div>
        </div>
    </div>
</div>

<script>
const apiKey = "YOUR_API_KEY";
const apiURL = "https://api.openweathermap.org/data/2.5/weather?&units=imperial&q=";

const searchBox = document.querySelector(".search input");
const searchBtn = document.querySelector(".search button");
const weatherIcon = document.querySelector(".weather-icon");

async function checkWeather(city){
    const response = await fetch(apiURL + city + `&appid=${apiKey}`);

    if(response.status == 404){
        document.querySelector(".error").style.display = "block";
        document.querySelector(".weather").style.display = "none";
    } else {
        var data = await response.json();

        document.querySelector(".city").innerHTML = data.name;
        document.querySelector(".temp").innerHTML = data.main.temp + "°F";
        document.querySelector(".humidity").innerHTML = data.main.humidity + "%";
        document.querySelector(".wind").innerHTML = data.wind.speed + " mp/h";

        if(data.weather[0].main == "Clouds"){
            weatherIcon.src = "images/clouds.png";
        }
        else if(data.weather[0].main == "Clear"){
            weatherIcon.src = "images/clear.png";
        }
        else if(data.weather[0].main == "Drizzle"){
            weatherIcon.src = "images/drizzle.png";
        }
        else if(data.weather[0].main == "Rain"){
            weatherIcon.src = "images/rain.png";
        }
        else if(data.weather[0].main == "Mist"){
            weatherIcon.src = "images/mist.png";
        }

        document.querySelector(".weather").style.display = "block";
        document.querySelector(".error").style.display = "none";
    }
}

searchBtn.addEventListener("click", ()=>{
    checkWeather(searchBox.value);
});
</script>

</body>
</html>
```

### `style.css`
```
*{ 
    margin: 0;
    padding: 0;
    font-family: 'Poppins', sans-serif;
    box-sizing: border-box;
}
body{ 
    background: #222;
}
.card{
    width: 90%;
    max-width: 470px;
    background: linear-gradient(135deg, #00feba, #5b548a);
    color: #fff;
    margin: 100px auto 0;
    border-radius: 20px;
    padding: 40px 35px;
    text-align: center;
}
.search{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.search input{
    border: 0;
    outline: 0;
    background: #ebfffc;
    color: #555;
    padding: 10px 25px;
    height: 60px;
    border-radius: 30px;
    flex: 1;
    margin-right: 16px;
    font-size: 18px;
}
.search button{
    border: 0;
    outline: 0;
    background: #ebfffc;
    border-radius: 50%;
    width: 60px;
    height: 60px;
    cursor: pointer;
}
.search button img{
    width: 16px;
}
.weather-icon{
    width: 170px;
    margin-top: 30px;
}
.weather h1{
    font-size: 80px;
    font-weight: 500;
}
.weather h2{
    font-size: 45px;
    font-weight: 400;
    margin-top: -10px;
}
.details{
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 20px;
    margin-top: 50px;
}
.col{
    display: flex;
    align-items: center;
    text-align: left;
}
.col img{
    width: 40px;
    margin-right: 10px;
}
.humidity, .wind{
    font-size: 28px;
    margin-top: -6px;
}
.weather{
    display: none;
}
.error{
    text-align: left;
    margin-left: 10px;
    font-size: 14px;
    margin-top: 10px;
    display: none;
}
