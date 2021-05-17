<!--template containing one root element to display weather information. -->
<template>
  <div class="weather-container">
    <div class="weather-wrap">
      <!--div to hold the search bar-->
      <div class="search-box">
        <input
          type="text"
          placeholder="Search..."
          class="search-bar"
         
          v-on:keypress="fetchWeather"
        />
      </div>
      <div class="weather-info">
        <!--div to hold the location information, city name/country-->
        <div class="location-box">
          <div class="location">
            {{ weather.name }}
          </div>
          <!--div to display today's date-->
          <div class="date">{{ todaysDate() }}</div>
        </div>
        <div class="weather-box">
          <!--div to contain the temperature, weather description and icon-->
          <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
          <div class="icon">
            <img:src="`${weather_icon}${weather.weather[0].icon}${'@2x.png'}`"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: 'Weatherbox',
  data() {
    return {
      //assigned variables for api key, api call, image
      api_key: "44cd4a31de2da1cbc8a7f43996818092",
      url_base: "https://api.openweathermap.org/data/2.5/",
      weather_icon: "http://openweathermap.org/img/wn/",
      query: "",
      weather: {},
    };
  },
  methods: {
    //api call using fetchWeather
   // async fetchWeather(e) {
    //  if (e.key == "Enter") {
    //    let response = await axios.get(
     //     `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
     //   );
     //   this.setResults(response.data);
     //   console.log(response.data);
     // }
   // },
    setResults(returnedResponse) {
      this.weather = returnedResponse;
    },
    //method to display date
    todaysDate() {
      const months = [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec",
      ];

      const days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
      let d = new Date();
      let month = months[d.getMonth()];
      let day = days[d.getDay()];
      let date = d.getDate();
      let year = d.getFullYear();
      return `${month} ${date} ${day} ${year}`;
    },
  },
  mounted(){
    axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
    .then((response) => {
      this.setResults = response.data;
      console.log(response.data);


    })

  }
};
</script>
<!--so much style css for component-->
<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Arial";
}
.weather-container {
  background-image: url("../assets/headerBG.jpeg");
  background-size: cover;
  background-position: center;
  transition: 0.4s;
  width: 375px;
  margin: 0 auto;
  border-radius: 25px;
  margin-top: 50px;
  box-shadow: 0px 0px 30px black;
}

.weather-wrap {
  height: 600px;
  padding: 25px;
  border-radius: 25px;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.15),
    rgba(0, 0, 0, 0.4)
  );
}
.search-box,
.search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  background-color: rgba(255, 255 255, 0.5);
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rbga(255, 255, 255, 0.75);
}

.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  font-style: italic;
  text-align: center;
  margin-top: 30px;
}
.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rbga(0, 0, 0, 0.25);
  background-color: rgba(255, 255 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  font-style: italic;
}

.weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
