<template>
  <div class="home" :style="{ 'backgroundImage': backgroundImage }">
    <form class="ui form">
      <div class="field">
        <label>City name</label>
        <input type="text" placeholder="City name" v-model="citySearched">
      </div>
      <button class="ui blue button" @click.prevent="getWeatherByCityName">Rechercher</button>
    </form>

    <div class="ui card" v-if="data">
      <div class="content">
        <div class="header">
          {{ data.name }}
        </div>
        <div class="meta">
          {{ data.sys.country }} <i class="flag" :class="data.sys.country|lowercase"></i>
        </div>
        <div class="description">
          {{ data.weather[0].main }}
        </div>
      </div>
      <div class="extra content">
        <div class="ui green message">Min T : <strong>{{ data.main.temp_min }} °C</strong></div>
        <div class="ui red message">Max T : <strong>{{ data.main.temp_max }} °C</strong></div>
      </div>
    </div>

    <div class="ui negative message" v-if="error">
      <i class="close icon" @click="error = !error"></i>
      <div class="header">
        <p>{{ error.cod }} : {{ error.message }}</p>
      </div>
    </div>

    <!--<pre>{{ data }}</pre>-->
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
      error: '',
      backgroundImage: ''
    }
  },
  methods: {
    getWeatherByCityName () {
      // GET weather with city by name
      this.$http.get(`http://api.openweathermap.org/data/2.5/weather?q="${this.citySearched}"&units=metric&APPID=96721a29bd0911ed5b1120957b462d69`)
      .then((response) => {
        // success callback
        console.log('success callback')

        // if error has old error, clear data
        if (this.error) {
          this.error = ''
        }

        this.data = response.body
        this.backgroundImage = 'url("static/images/' + this.data.weather[0].main.toLowerCase() + '.jpg")'
      }, (error) => {
        // error callback
        console.log('error callback')

        // if data has old data, clear data
        if (this.data) {
          this.data = ''
          this.backgroundImage = ''
        }

        this.error = error.body
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.home {
  height: inherit;
}
.form {
  width: 50%;
  margin: 0 auto;
  padding-top: 100px;
}
.field {
  width: 100%;
}
.negative .message {
  width: 50%;
  margin: 15px auto;
}
.card {
  margin: 15px auto;
  background-color: rgba(255, 255, 255, 0.5);
}
</style>
