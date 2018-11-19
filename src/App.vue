<template>
  <div id="app">
    <img src="./assets/logo.png" height="10%" width="10%">
    <h1>{{msg}}</h1>
    <hr>
    <b-container class="bv-example-row">
      <b-row>
        <b-col cols="3"><Region></Region></b-col>
        <b-col cols="3"><Departement></Departement></b-col>
        <b-col cols="3"><Commune></Commune></b-col>
        <b-col cols="3"><Information></Information></b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
  import Region from "./Region"
  import Departement from "./Departement" 
  import Commune from "./Commune"
  import Information from "./Information"
  import $ from "jquery"
  import Bootstrap from "bootstrap"
  export default {
    name: 'app',
    data () {
      return {
        msg: 'Régions, Départements, et Communes de France'
      }
    },  
    components: {
      Region,
      Departement,
      Commune,
      Information
    }
  }

</script>

<style>
#app {
  text-align: center;
}

h1 {
  font-weight: normal;
  margin-bottom: 5%;
  margin-top: 5%;
}
</style>
