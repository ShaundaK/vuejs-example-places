<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="place in places">
      <h3>{{ place.name }}</h3>
      <h4>{{ place.address }}</h4>
    </div>
  </div>
</template>

<style>
</style>

<script>
  var axios = require('axios');
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      places: []
    };
  },
  created: function() {
    console.log('in the created function');
    console.log(this)
    axios.get('http://localhost:3000/api/places').then(function(response) {
      console.log(response.data);
      this.places = response.data;
    }.bind(this))
  },
  methods: {},
  computed: {}
};
</script>
