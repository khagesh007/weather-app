<template>
  <Rain :weather="weather"></Rain>
  <Content :query="query" msg="Welcome to Your Vue.js App">
    <template v-slot:formdata >
      <div class="search-box">
        <input type="text" class="search-bar"
               v-model="query"
               placeholder="Search by location"
               @keypress.enter="getWeatherData"
        >

      </div>

      <Clouds :weather="weather" ></Clouds>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{Math.round(weather.main.temp)}}°c</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
      </div>
    </template>
  </Content>

</template>

<script>
import Content from './components/Content.vue'
import Clouds from './components/Clouds.vue'
import Rain from './components/Rain.vue'


export default {
  name: 'App',
  components: {
    Clouds,
    Content,Rain
  },
  data(){
    return {
      api_key : 'eee4561c87943fbc03298e6d16ea2de0',
      api_url : '',
      query : '',
      weather: {}
    }
  },
  methods : {
    getWeatherData () {

        fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res=>{
          return res.json();
        }).then(this.setResults);

    },
    setResults(results){
      this.weather = results;

    }
  }
}
</script>

<style>
#app {
  /*background-image: url('./assets/cold-weather-bg.jpg');*/
}
#app{
  font-family: 'montserrat', sans-serif;
  background-image: url('./assets/cold-weather-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/*#app {*/
/*  background-image: url('./assets/cold-bg.jpg');*/
/*  background-size: cover;*/
/*  background-position: bottom;*/
/*  transition: 0.4s;*/
/*}*/
#app.warm {
  background-image: url('./assets/cold-weather-bg.jpg');
}
main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
  z-index: 10;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;
  appearance: none;
  border:none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location {
  color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: #FFF;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #FFF;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color:rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  color: #FFF;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
