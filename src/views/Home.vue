<template>
  <div class="home">
    <h1>{{ message }}</h1>
    Search by name: <input v-model="nameFilter" list ="places">
    <!-- Search by bio: <input v-model="nameFilter" list="bios"> -->
    <datalist id="places">
      <span v-for="place in places">
        <option>{{place.name}}</option>
        <option>{{place.address}}</option>
      </span>
    </datalist>

    <div v-for="place in filterBy(places, nameFilter, 'name')">
      <h3>{{ place.name }}</h3>
      <h4>{{ place.address }}</h4>
    </div>
  </div>
</template>

<style>
</style>

<script>
  var axios = require('axios');
  import Vue2Filters from 'vue2-filters'
 export default {
  mixins: [Vue2Filters.mixin], 
  data: function() {
    return {
      message: "Places",
      places: [],
      nameFilter: ''
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
  methods: {
    addPlace: function() {
      var params = {
        name: this.NewPlace.name,
        address: this.NewPlace.address
      }
      axios.get("http://localhost:3000/api/places", params).then(function(response) {
        console.log("response.data");
        this.places.push(response.data);
      }.bind(this))
    }
  },
  
  computed: {}
};
</script>
