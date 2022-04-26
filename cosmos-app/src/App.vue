<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp < 70 ? 'earth' : ''">
    <h1>Cosmos App</h1>
    <main >
      <div class="search-box">
        <input type="text"
        class="search-bar"
        placeholder="search...." 
        v-model="query"
        v-on:keypress="fetchWeather"
        />
        <!-- fetchWeather calls to method -->
         <!-- two way binding to data -->
   
      </div>


    <div class="weather-wrap" id="earth" v-if="typeof weather.main != 'undefined' ? 'sun' : '' ">
      <div class="location-box" style="color:rgb(13, 13, 107)">
        <div class="location" style="color:rgb(184, 239, 247); font-weight:bold">{{ weather.name }}, {{ weather.sys.country }}</div>
         <!-- city and country are bound from api -->
        <div class="date" style="color:rgb(184, 239, 247); ">{{ dateBuilder() }}</div>
        <div class="sunrise">{{ weather.sys.sunrise }}~Sunrise time in UTC</div>
        <div class="sunset">{{ weather.sys.sunset }}~Sunset time in UTC</div>
 
      </div>
    </div>


    <!-- <div class="weather-box"> -->
      <!-- <div class="temp">{{ Math.round(weather.main.temp) }}°C</div> -->
      <!-- math.round rounds temps to whole number -->
      <!-- <div class="weather">{{ weather.weather[0].main }}</div> -->
    <!-- </div> -->
    <div class="utc-container">
      <div class="utc">
        <h3>What is UTC?</h3>
        <p>
        Coordinated Universal Time (UTC) is the basis for civil time today. This 24-hour time standard is kept using highly precise atomic clocks combined with the Earth's rotation.
        Universal Time (UT) was created at the International Meridian Conference in 1884. This is the basis for the 24-hour time zone system we know today. While in space, NASA uses UTC!
        </p>
      </div>
    </div>
    

   <div class="facts-container">
    <div class="astronaut-facts">
      <h3 style="color:rgb(13, 13, 107)">Did you know?</h3>
      <p style="color:rgb(13, 13, 107); font-weight:bold" >Did you know the ISS (International Space Station) space station is capable of getting deliveries? In fact, there have been multiple deliveries
        to the ISS including one from Pizza Hut!
      </p>
      
    </div>
    </div>
  </main>
  <footer>~Created by Nasya Gay 2022.~</footer>
 </div>
</template>

<script>


export default {
  name: 'App',
  data () {
    return {
      api_key: '81a145652bc68fa404e511488d37190d',
      // api key for weather
      url_base: 'https://api.openweathermap.org/data/2.5/',
      // api base
      query: '',
      weather: {}
    }
  },
  methods: {
     fetchWeather (e) {
       if (e.key == "Enter") {
        //  event listener for pressing enter
         fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        //  gets data from api by passing the query bound to searchbox
        .then((data)  => {
          return data.json();
        }).then(this.setResults);
       }
      
     },
     setResults (results) {
       this.weather = results;
     },
      
     dateBuilder () {
        let d = new Date();
        let months = ["January", "February", "March", "April", "May", "June", "July", "August",
        "September", "October", "November", "December"];
        let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday",
        "Saturday"];

        let day = days[d.getDay()];
        let date = d.getDate();
        let month = months[d.getMonth()];
        let year = d.getFullYear();

        return `${day} ${date} ${month} ${year}`;
     }
  }


}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: 'montserrat', sans-serif;
}
h1{
  color:rgb(184, 239, 247);
  font-size: 48px;
  text-shadow: 1px 3px rgba(184, 239, 247, 0.26);
}
#app {
 
 background-image: url('./assets/Sun.jpg');
 background-size: cover;
 background-position: bottom;
 transition: 0.4s;
}

#app.earth {
  background-image: url('./assets/earth.jpg');
}
main{
  /* display: flex;
  flex-direction: row;
  justify-content: center; */
  min-height: 100vh;
  padding: 25px;
}
.search-box .search-bar {
  /* display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center; */

  width: 100;
  margin-bottom: 30px;
  padding: 15px;

  color: azure;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(184, 239, 247, 0.26);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.search-bar .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location{
 display: flex;
 flex-direction: column;
 padding: 1rem; 
 /* "clamp-card layout" */
 color: whitesmoke;
 font-size: 38px;
 font-weight: 500;
 text-align:center;
 text-shadow: 1px 3px rgba(184, 239, 247, 0.26);
}
.weather-wrap{


  color: azure;
}
.location-box .date{
 color: whitesmoke;
 font-size: 20px;
 font-weight: 300;
 text-align:center;
 font-style: italic;

}
.weather-box{
  color: azure;
  text-align:center;

}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: azure;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(184, 239, 247, 0.26);
  background-color: rgba(184, 239, 247, 0.26);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(184, 239, 247, 0.26);;
}

.weather-box .weather {
  color: azure;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(184, 239, 247, 0.26);


}
.facts-container{
   display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
 
}
.utc-container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.utc{
 color:rgb(13, 13, 107);
 font-size: 20px;
 font-weight: bold;
 text-align:center;
 font-style: italic;
 width: 300px;
 margin-bottom: 30px;
 padding: 15px;

  background-color: rgba(163, 226, 236, 0.431);
  border-radius: 16px;
  margin: 30px 0px;
}
.astronaut-facts{
 color:azure;
 font-size: 20px;
 font-weight: bold;
 text-align:center;
 font-style: italic;
 width: 300px;
 margin-bottom: 30px;
 padding: 15px;

  background-color: rgba(163, 226, 236, 0.431);
  border-radius: 16px;
  margin: 30px 0px;
}
h3 {
   text-decoration: underline;
}
p{
  margin-top: 0.5rem;
  font-size: 15px;
}
.sunrise{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
 
 color: rgb(243, 220, 92);
 padding:5px;
}
.sunset{
 display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
 
 color: rgb(243, 220, 92);
 padding: 5px;
}
footer{
  color:rgb(184, 239, 247);
  font-size: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
 
}
</style>

