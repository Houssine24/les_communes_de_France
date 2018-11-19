<template>
  <div id="app_5">
    <h3>{{msg}}</h3>
    <hr>
  <div v-for="e in info">
    <b-list-group>
        <b-list-group-item>Ville : <p>{{e.nom}}</p></b-list-group-item>
        <b-list-group-item>Code postal <p>{{e.codesPostaux}}</p></b-list-group-item>
        <b-list-group-item>Population de <p>{{e.population}} habitants</p></b-list-group-item>
        <b-list-group-item>Surface de <p>{{e.surface}} m²</p></b-list-group-item>
    </b-list-group>
  </div>
</div>
</template>

<script>
  import $ from "jquery"
  import Bootstrap from "bootstrap"
  export default {
    name: 'app_5',
    data () {
      return {
        msg: 'Informations',
        info: []
      }
    },
    mounted(){
      this.$root.$on('blabla', data => {
        fetch('https://geo.api.gouv.fr/communes?code='+data+'&fields=nom,code,codesPostaux,surface,population&format=json&geometry=centre')
        .then(response => response.json())
        .then(json => {
          this.info = json
        })
      })
    }
  }

</script>

<style>
  p{
    justify-content: space-around;
    color: blue;
  }
</style>