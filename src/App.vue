<template>
  <div id="app">
    <main>
      <div class="search">
        <input type="text" name="" id="" class="search-bar" placeholder="Suche.." v-model="query" @keypress="fetchWeather"/>
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{weather.name}}, {{weather.sys.country}}
          </div>
          <div class="date">
            {{dateBuilder()}}
          </div>
          <div class="weather-box">
            <div class="temp">{{Math.round(weather.main.temp)}}°C</div>
            <div class="weather">{{weather.weather[0].main}}</div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: "App",
  data() {
    return {
      api_key: 'ade039d1e0e84993e1444c05dfee1b08',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather(e) {
      if (e.key == 'Enter') {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);

        this.query=""
      }
    },
    setResults(results) {
      this.weather = results;
    },
    dateBuilder() {
      let d = new Date();
      let months = [
      "January",
      "February",
      "March",
      "April",
      "May",
      "June",
      "July",
      "August",
      "September",
      "October",
      "November",
      "December"
      ];
      let days = [
      "Monday",
      "Tuesday",
      "Wednesday",
      "Thursday",
      "Friday",
      "Saturday",
      "Sunday"
      ];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()]
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`
    }
  }
  
};
</script>

<style lang="scss">
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  html {
    font-size: 16px;
  }

  body {
    font-family: 'montserrat', sans-serif;
  }

  #app {
    background-image: url('../src/assets/img/daniel-ramirez-q4TfWtnz_xw-unsplash.jpg');
    background-size: cover;
    background-position: bottom;
    height: 100vh;

    main {
      min-height: 100vh;
      padding: 1.6rem;

      /* gradient */
      background-image: linear-gradient(to bottom, rgba(0,0,0, .1), rgba(0,0,0, .3));

      .search {

        .search-bar {
          display: block;
          width: 100%;
          padding: .9rem;

          color: #313131;
          font-size: 1.2rem;

          appearance: none;
          border: none;
          outline: none;
          background: none;

          box-shadow: 0 0 .5rem rgba(0,0,0,0.25);
          background-color: rgba(255,255,255, .5);
          border-radius: 0 1rem 0 1rem;

          transition: .4s;

          &:focus {
            box-shadow: 0 0 .1rem rgba(0,0,0,0.25);
            background-color: rgba(255,255,255, .75);
            border-radius: 1rem 0 1rem 0;
          }
        }
      }

      .location-box {

        .location {
          color: #fff;
          font-size: 2rem;
          font-weight: 500;
          text-align: center;
          text-shadow: .06rem .18rem rgba(0,0,0,0.25);

          padding-top: 2rem;
        }

        .date {
          color: #fff;
          font-size: 1.25rem;
          font-weight: 300;
          text-align: center;
          font-style: italic;
        }

        .weather-box {

          text-align: center;
          .temp {
            display: inline-block;
            padding: 1.6rem 1.25rem;
            color: #fff;
            font-size: 6.3rem;

            text-shadow: .18rem .32rem rgba(0,0,0,0.25);
            background-color: rgba(255,255,255, .25);
            border-radius: 1rem;
            margin: 2rem 0;
          }

          .weather {
            color: #fff;
            font-size: 3rem;
            font-weight: 700;
            font-style: italic;
            text-shadow:  .18rem .32rem rgba(0,0,0,0.25);
          }
        }
      }
    }
    }
</style>
