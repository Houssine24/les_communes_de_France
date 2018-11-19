<template>
  <div id="app_4">
    <h3>{{msg}}</h3>
    <p class="select">{{msg_bis}}</p>
    <hr>
    <b-input class="mb-2 mr-sm-2 mb-sm-0" v-model="search" id="inlineFormInputName2" placeholder="Rechercher une commune" />
  <div class="affichageComm" v-for="e in filteredCommune">
    <b-button
      variant="light"
      v-on:click="getInfo"
      v-bind:key="e.nom"
      v-bind:value="e.code">{{e.nom}}
    </b-button>
  </div>
</div>
</template>

<script>
  import $ from "jquery"
  import Bootstrap from "bootstrap"
  export default {
    name: 'app_4',
    data () {
      return {
        msg: 'Commune',
        msg_bis: '*sélectionner une commune',
        commune: [],
        search:''
      }
    },
    mounted(){
      this.$root.$on('coucou', data => {
        fetch('https://geo.api.gouv.fr/departements/'+data+'/communes?fields=nom,code')
        .then(response => response.json())
        .then(json => {
          this.commune = json
        })
      })
    },
    computed: {
        filteredCommune: function(){
          return this.commune.filter((e)=>{
            return e.nom.match(this.search);
          });
        }
    },
    methods: {
      getInfo: function(e) {
        console.log(e.target.value)
        this.$root.$emit('blabla', e.target.value)
      }
    }
  }

</script>

<style>
  .mb-2{
    text-align: center;
  }

  .affichageComm{
    margin-top: 5%;
  }
</style>