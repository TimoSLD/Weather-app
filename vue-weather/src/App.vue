<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Search..." v-model="query" @keypress="fetchWeather">
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }} , {{ weather.sys.country }}</div>

          <div class="weather-box">
            <div class="temp">{{ Math.round(weather.main.temp) }}</div>
            
     
          </div>
        </div>
      </div>

    </main>
  </div>
</template>

<script>


export default {
  name: 'App',
  data () {
    return {
      api_key: '5b15042c478deab9bebc49a7c118b49b',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
      }
    },
    setResults (results) {
      this.weather = results;
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

body{
  font-family: 'montserrat', sans-serif;
}

#app {
  background-image: url('./assets/night (1).png');
  background-size: cover;
}

main{
  min-height: 100vh;
  padding: 25px;
}

.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  border: none;
  outline: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  border-radius: 16px 16px 16px 16px;

}

.search-box .search-bar:focus{
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 32px 32px 32px 32px;
}

.location-box .location{
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow:1px 3px rgba(0, 0, 0, 0.25);
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

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
