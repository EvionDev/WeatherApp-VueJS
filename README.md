# WeatherApp-VueJS

WeatherApp is a weather application built using Vue.js and Tailwind CSS. It allows users to check the current weather, including information about the weather conditions (cloudy, sunny, etc.) and the feels-like and basic temperatures. The app utilizes an external weather API (https://api.weatherapi.com) to fetch the latest weather data. Based on this data, WeatherApp displays the weather conditions, such as sky condition, as well as the feels-like and basic temperatures.

## Live preview

[https://eviondev-weatherapp.netlify.app](https://eviondev-weatherapp.netlify.app)

## Installation and Configuration Guide

1. Get your api key from [weatherapi.com](https://weatherapi.com)

2. Clone the application repository from GitHub or download zip.
#### `git clone https://github.com/EvionDev/WeatherApp-VueJS.git`

3. Navigate to the application directory.
#### `cd weather-app`

4. Create file .env.
#### `touch .env`

5. Open the .env file and enter your API key for the weather service in the appropriate place.
#### `VITE_API_KEY=YOUR_KEY`

6. Install the application dependencies and run the application in development mode.
#### `npm i && npm run dev`
