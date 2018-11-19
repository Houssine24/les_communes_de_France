<template>
  <div id="app_3">
    <h3>{{msg}}</h3>
    <p class="select">{{msg_bis}}</p>
    <hr>
    <b-input class="mb-2 mr-sm-2 mb-sm-0" v-model="search" id="inlineFormInputName2" placeholder="Rechercher un département" />
    <div class="affichageDep" v-for="e in filteredDepartement">
      <p>
        <b-button
          variant="light"
          v-on:click="getCommune"
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
        msg: 'Département',
        msg_bis: '*sélectionner un département',
        departement: [],
        search:''
      }
    },
    computed: {
        filteredDepartement: function(){
          return this.departement.filter((e)=>{
            return e.nom.match(this.search);
          });
        }
    },
    mounted(){
      this.$root.$on('salut', data => {
        fetch('https://geo.api.gouv.fr/regions/'+data+'/departements?fields=nom,code')
        .then(response => response.json())
        .then(json => {
          this.departement = json
        })
      })
    },
    methods: {
      getCommune: function(e) {
        console.log(e.target.value)
        this.$root.$emit('coucou', e.target.value)
      }
    }
  }
</script>

<style>
  .mb-2{
    text-align: center;
  }

  .affichageDep{
    margin-top: 5%;
  }
</style>
