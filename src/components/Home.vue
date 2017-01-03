<template>
  <div class="home">
    <form class="ui form">
      <div class="field">
        <label>City name</label>
        <input type="text" placeholder="City name" v-model="citySearched">
      </div>
      <button class="ui blue button" @click.prevent="getWeatherByCityName">Rechercher</button>
    </form>
    <div class="ui cards" v-if="data">
      <div class="card">
        <div class="content">
          <!--<img class="right floated mini ui image" src="/images/avatar/large/jenny.jpg">-->
          <div class="header">
            {{ data.name }}
          </div>
          <div class="meta">
            {{ data.sys.country }}
          </div>
          <div class="description">
            <!--{{ data.weather[0].description }}-->
          </div>
        </div>
        <div class="extra content">
          <div class="ui two buttons">
            <div class="ui basic green button">{{ data.main.temp_min }} °C</div>
            <div class="ui basic red button">{{ data.main.temp_max }} °C</div>
          </div>
        </div>
      </div>
    </div>

    <div class="ui negative message" v-if="error">
      <i class="close icon" @click="error = !error"></i>
      <div class="header">
        <p>{{ error.cod }} : {{ error.message }}</p>
      </div>
    </div>

    <pre>{{ data }}</pre>
    <!--<pre>{{ error }}</pre>-->
  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      data: '',
      citySearched: '',
      error: ''
    }
  },
  methods: {
    getWeatherByCityName () {
      // GET weather with city name
      this.$http.get('http://api.openweathermap.org/data/2.5/weather?q=' + this.citySearched + '&units=metric&APPID=96721a29bd0911ed5b1120957b462d69')
      .then((response) => {
        // success callback
        console.log('success callback')

        // if error has old error, clear data
        if (this.error) {
          this.error = ''
        }

        this.data = response.body
      }, (error) => {
        // error callback
        console.log('error callback')

        // if data has old data, clear data
        if (this.data) {
          this.data = ''
        }

        this.error = error.body
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#app .h1 {
  margin: 0 auto;
  text-align: center;
}
.form {
  width: 50%;
  margin: 0 auto;
}
.field {
  width: 100%;
}
</style>
