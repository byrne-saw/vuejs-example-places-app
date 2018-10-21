<template>
  <div class="home">
    <h1>All the Places</h1>


    <div v-for="place in places">
      <h2>{{ place.name }}</h2>
      <h3>{{ place.address }}</h3>     
    </div>

    <div>
      Name: <input v-model="newPlace.name">
      Address: <input v-model="newPlace.address">
      <button @click="addPlace()">New Place</button>
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
      places: [],
      newPlace: {name: "", address: ""}
    };
  },
  created: function() {
    axios
    .get("http://localhost:3000/api/places")
    .then(function(response) {
      this.places = response.data;
    }.bind(this));


  },
  methods: {
    addPlace: function () {
      var params = {
                   name: this.newPlace.name,
                   address: this.newPlace.address
                   };
      axios
      .post("http://localhost:3000/api/places", params)
      .then(function(response) {
        this.places.push(response.data);
        this.newPlace = {name: "", address: ""};
      }.bind(this));                   
    }
  },
  computed: {}
};
</script>