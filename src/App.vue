<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <Test v-bind:artists="artists"/> -->
    <div>
  <b-button v-b-modal.modal-1>Launch demo modal</b-button>
  <b-modal id="modal-1" title="BootstrapVue">
   <template #default="{ ok }">
    <p class="my  -4">
      <input type="text" v-model="itemText.name" placeholder="Adicione um artista!" />
      <input type="text" v-model="itemText.country" placeholder="Adicione a cidade dele!" />
      <button v-on:click="addItem(), ok()" class="btn btn-primary btn-sm">Adicionar</button>
    </p>
   </template>
  </b-modal>
</div>
    <Test2 v-bind:artists="artists" @changeMsg3="setMessage" :msg="itemText2"/>
  </div>
</template>
<script>
// import Test from './components/Test.vue'
import Test2 from './components/Test2'
export default {
  name: 'app',
  components: {
    // Test,
    Test2,
  },
  data (){
    return {
      itemText2: {name: '', country: ''},
      artists: [
       {name: 'Davido', genre: 'afrobeats', country: 'Nigeria'},
       {name: 'Burna Boy', genre: 'afrobeats', country: 'Nigeria'},
       {name: 'AKA', genre: 'hiphop', country: 'South-Africa'},
       // {name: 'Sarkodie', genre: 'hiphop', country: 'Ghana'},
       // {name: 'Stormzy', genre: 'hiphop', country: 'United Kingdom'},
       // {name: 'Lil Nas', genre: 'Country', country: 'United States'},
       // {name: 'Nasty C', genre: 'hiphop', country: 'South-Africa'},
       // {name: 'Shatta-walle', genre: 'Reagae', country: 'Ghana'},
       // {name: 'Khalid', genre: 'pop', country: 'United States'},
       // {name: 'Ed Sheeran', genre: 'pop', country: 'United Kingdom'}
     ],
      itemText: {name: '', country:''}
    }
  },
  methods: {
    addItem: function() {
      var itemTextContent
      itemTextContent = this.itemText
      if(!itemTextContent){return;}
      this.artists.push(itemTextContent)
      this.itemText = {name: '', country:''}
    },
  // addItem: function() {
  //   var itemTextContent
  //   if(this.itemText.name){
  //   console.log("Foco a")
  //   itemTextContent = this.itemText
  //   this.itemText2 = {name: '', country:''};}
  //   if(this.itemText2.name){
  //   console.log("Foco b")
  //   itemTextContent = this.itemText2}
  //   if(!itemTextContent){return;}
  //   this.artists.push(itemTextContent)
  //   this.itemText = {name: '', country:''}
  // },
  removeItem: function(x) {
    this.artists.splice(x, 1);
    // console.log(String(x))
  },
  changeItem: function(x) {
    var itemTextContent2
    itemTextContent2 = this.itemText2
    if(!itemTextContent2){return;}
    this.artists.splice(x, 1, itemTextContent2);
    // this.itemText2 = {name: '', country:''}
  },
  setMessage: function(msg) {
    this.itemText2 = msg;
    console.log('teste123')
  },
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
