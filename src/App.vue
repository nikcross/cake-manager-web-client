<template>
  <div id="app" class="grid-container">
    <div class="grid-x grid-padding-x">

      <div class="large-12 cell">
        <h1>The Cake Manager <span>{{version.text}}</span></h1>
      </div>

        <div class="card" v-for="cake in cakes" v-bind:key="cake.title">
          <div class="card-divider">{{ cake.title }}</div>
          <div class="card-image"><img :src="cake.image"></div>
          <div class="card-section">{{ cake.description }}</div>
        </div>

    </div>

    <CakeForm @addCakeEvent="addACake"/>

  </div>
</template>

<script>

import CakeForm from './components/CakeForm.vue'

function addCake(cake) {

  fetch("http://localhost:8080/cakes", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify(cake)
  })
      .then(response => {
        if (response.ok) {
          updateCakes();
        } else {
          alert("Server returned " + response.status + " : " + response.statusText);
        }
      }).catch(err => {
    console.log(err);
  });
  return false;
}

function updateCakes() {
  fetch("http://localhost:8080/cakes", {
    method: "GET",
    headers: {}
  })
      .then(response => {
        if(response.ok){
          return response.json()
        } else{
          alert("Server returned " + response.status + " : " + response.statusText);
        }
      }).then(response => {
        cakes.splice(0,cakes.length);
        for(let i in response) {
          cakes.push(response[i]);
        }
  })
      .catch(err => {
        console.log(err);
      });
}

function getVersion() {
  fetch("http://localhost:8080/version", {
    method: "GET",
    headers: {}
  })
      .then(response => {
        if(response.ok){
          return response.json();
        } else{
          alert("Server returned " + response.status + " : " + response.statusText);
        }
      }).then(response => {
    version.text = response.text;
  })
      .catch(err => {
        console.log(err);
      });
}

let cakes = [];
let version = { text: "loading..." };

export default {
  name: 'App',
  components: {
      CakeForm
  },

  methods: {
    addACake(cake) {
        addCake(cake);
    }
  },

  data() {
    return {
      cakes: cakes,
      version: version
    };
  },

  beforeMount() {
    getVersion(version);
    updateCakes();
  }
};
</script>

<style>
@import './assets/css/app.css';
@import './assets/css/foundation.css';

body {
  margin: 20px;
}

.card {
  width: 300px;
  margin: 20px;
  border-radius: 10px;
}

.card img {
  min-height: 300px;
}
</style>
