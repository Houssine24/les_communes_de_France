<template>
  <div id="app_3">
    <h3>{{msg}}</h3>
    <p class="select">{{msg_bis}}</p>
    <hr>
    <b-input class="mb-2 mr-sm-2 mb-sm-0" v-model="search" id="inlineFormInputName2" placeholder="Rechercher une région"/>
    <div class="affichageReg" v-for="e in filteredRegion">
      <p>
        <b-button
          variant="light"
          v-on:click="getDepartement"
          v-bind:key="e.nom"
          v-bind:value="e.code">{{e.nom}} 
        </b-button>
      </p>
    </div> 
  </div> 
</template>

<script>
  import $ from "jquery"
  import Bootstrap from "bootstrap"
  export default {
    name: 'app_3',
    data () {
      return {
        msg: 'Région',
        msg_bis: '*sélectionner une région',
        region: [],
        search:''
      }
    },
    computed: {
        filteredRegion: function(){
          return this.region.filter((e)=>{
            return e.nom.match(this.search);
          });
        }
    },
    created(){
      fetch('https://geo.api.gouv.fr/regions?fields=nom,code')
      .then(response => response.json())
      .then(json => {
        this.region = json
      });
    },
    methods: {
      getDepartement: function(e) {
        console.log(e.target.value)
        this.$root.$emit('salut', e.target.value)
      }
    }
  }
</script>

<style>
  .select{
    text-align: center;
    color: red;
  }
  .mb-2{
    text-align: center;
  }

  .affichageReg{
    margin-top: 5%;
  }
</style>