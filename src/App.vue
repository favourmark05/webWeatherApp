<template>
  <div id="app" :class="typeof weather.main != 'undefined' &&  weather.main.temp >= 20 ? 'warm' : ''">
    <main>
      <div class="search-box">
        <input 
        type="text"  
        class="search-bar" 
        placeholder="search..."
        v-model="query"
        @keypress="fetchWeather"
        />
        <button @click="fetchWeather" class="button">search</button>
      </div>
      <div class="wearther-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ currentDate() }}</div>

          <div class="weather-box">
            <div class="temp">{{ Math.round(weather.main.temp) }}&deg;c</div>
            <div class="weather">{{ weather.weather[0].main }}</div>
          </div>
        </div>
      </div>
      <div class="credit">
        <h2>App built by <a href="https://mfonidomark.netlify.app/" target="_blank" rel="noopener noreferrer">Mfonido Mark</a></h2>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      api_key: '518057da23984794218d2e894e323698',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather (e) {
      if (e.key == "Enter" || Event ) {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
          // return console.log(res.json())
        }).then(this.setResults);
    }
    },
    setResults (results) {
      this.weather = results;
    },
    currentDate () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September",
      "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

      let day =days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    }
  }
  
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  font-family: 'montsrrat', sans-serif;
}
#app{
  background-image: url('https://media.giphy.com/media/BDucPOizdZ5AI/giphy.gif');
  /* background-repeat: no-repeat; */
  background-size: cover;
  background-position: bottom;
  /* height: 100vh; */
  transition: 0.4s;
}

#app.warm{
  background-image: url('https://media.giphy.com/media/paMdZlRXlc96o/giphy.gif');
  background-size: cover;
  background-position: bottom;
  /* height: 100vh; */
  transition: 0.4s;
}
main{
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.25),rgba(0,0,0,0.75));
}
.search-box{
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  background-color: rgba(255,255,255,0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
  box-shadow: 0px 0px 8px rgba(0,0,0,0,0.25);
}

.search-box .search-bar:focus {
  background-color: rgba(255,255,255,0.75);
  box-shadow: 0px  0px 16px rgba(0,0,0, 0.25);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0, 0.25);
}
.location-box .date{
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  text-align: center;
  font-style: italic;
}
.weather-box{
  text-align: center;
}
.weather-box .temp{
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0,0,0, 0.25);
  background-color: rgba(255,255,255,0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0,0,0,0.25);
}
.weather-box .weather{
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0,0,0, 0.25);
}

.credit{
  color: rgb(6, 209, 182);
  text-align: center;
  padding: 10px 25px;
}
.credit > h2 > a {
  color: white;
}
.button{
  background-color: rgb(24, 158, 151);
  color: white;
  border: 4px solid rgb(24,158,151);
  border-radius: 10px;
  padding: 10px 10px 10px 10px;
  margin: 10px 25px;
  cursor:pointer;
  /* font-style: bold; */
}
</style>
