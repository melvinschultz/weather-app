<template>
  <div class="home">
    <form class="ui form">
      <div class="field">
        <label>City name</label>
        <input type="text" placeholder="City name" v-model="city.name">
      </div>
      <button class="ui blue button" @click.prevent="getWeatherByCityName">Rechercher</button>
    </form>
    <pre>{{ response.body }}</pre>
  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      city: {
        name: ''
      },
      response: []
    }
  },
  methods: {
    getWeatherByCityName () {
      // GET weather with city name
      this.$http.get('http://api.openweathermap.org/data/2.5/weather?q=' + this.city.name + '&APPID=96721a29bd0911ed5b1120957b462d69')
      .then((response) => {
        // success callback
        console.log('success callback')
        console.log(response)
        this.response = response
      }, (response) => {
        // error callback
        console.log('error callback')
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
