<template>
  <div class="home">
    <h1>Wie wird das Wetter, Quaxo?</h1>
    <div class="search-box">
      <input
        type="text"
        class="search-bar"
        placeholder="Hier kannst du einen Ort eingeben.."
        v-model="query"
        @keypress="fetchWeather"
      />
    </div>
    <Cities msg="Wähle eine Stadt aus" @citySelect="setCity" />
    <img class="quaxo" v-bind:src="pokemon_urls.quaxo" alt="Quaxo" />
    <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
      <div class="location-box">
        <div class="location">
          {{ weather.name }}, {{ weather.sys.country }}
        </div>
        <div class="date">{{ dateBuilder() }}</div>
      </div>

      <div class="weather-box">
        <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
        <div class="weather">
          Gefühlt: {{ Math.round(weather.main.feels_like) }}°C
        </div>
        <!-- <div class="weather">{{ weather.weather[0].main }}</div> -->
        <img :src="pokemon_urls.lugia" alt="" />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Cities from '@/components/Cities.vue'

export default {
  name: 'Home',
  components: {
    Cities,
  },
  data() {
    return {
      api_key: '18c5c2f50b243be5b8154718e223ce55',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
      http: 'https://css-tricks.com/',
      evoli_url: require('../assets/evoli.png'),
      quaxo_url: '../assets/quaxo2.png',
      pokemon_urls: {
        quaxo: require('../assets/quaxo2.png'),
        pikatchu: require('../assets/pikatchu.png'),
        evoli: require('../assets/evoli.png'),
        glumanda: require('../assets/glumanda.png'),
        lugia: require('../assets/lugia.png'),
      },
    }
  },
  methods: {
    fetchWeather(e) {
      console.log('fetchWeatcher function')
      if (e.key == 'Enter') {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json()
          })
          .then(this.setResults)
      }
    },
    setCity(e) {
      if (e.city)
        fetch(
          `${this.url_base}weather?q=${e.city}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json()
          })
          .then(this.setResults)
    },
    getPokemonUrl(res) {
      console.log('getPokemon function', res)
    },
    setResults(results) {
      const quaxo = document.querySelector('.quaxo')
      quaxo.classList.add('hidden')
      console.log('setResults function', results)
      this.weather = results
    },
    dateBuilder() {
      let d = new Date()
      console.log(d)
      let months = [
        'Januar',
        'Februar',
        'März',
        'April',
        'Mai',
        'Juni',
        'Juli',
        'August',
        'September',
        'Oktober',
        'November',
        'Dezember',
      ]
      let days = [
        'Sontag',
        'Montag',
        'Dienstag',
        'Mittwoch',
        'Donnerstag',
        'Freitag',
        'Samstag',
      ]
      let day = days[d.getDay()]
      let date = d.getDate()
      let month = months[d.getMonth()]
      let year = d.getFullYear()
      return `${day}, ${date}. ${month} ${year}`
    },
  },
}
</script>

<style scoped>
.home {
  min-height: 100vh;
  padding: 10px 25px;
  /* background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  ); */
}

h1 {
  padding: 20px 0 25px;
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 10px 15px;

  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
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

.quaxo.hidden {
  height: 0;
}

.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: #fff;
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
  color: #fff;
  font-size: 80px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  color: #fff;
  font-size: 40px;
  font-weight: 600;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box img {
  height: 250px;
}

.pokemon-img {
  border: 2px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  padding: 15px;
}
</style>
