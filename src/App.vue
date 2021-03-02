<template>
<div id="app">
  <Navbar />
  <div>
    <b-modal id="modal-1" title="BootstrapVue">
      <template #default="{ ok }">
        <p class="my  -4">
          <b-input input type="text" v-model="itemText.nome" placeholder="Adicione um meta!"></b-input>
          <b-button v-on:click="addItem(), ok()" variant="primary" class="btn btn-primary btn-sm">Adicionar</b-button>
        </p>
      </template>
    </b-modal>
  </div>
  <Test2 v-bind:metas="metas" @changeMsg3="setMessage" :msg="itemText2" />
</div>
</template>
<script>
// import Test from './components/Test.vue'
import Test2 from './components/Test2'
import Navbar from './components/Navbar'

export default {
  nome: 'app',
  components: {
    // Test,
    Test2,
    Navbar,
  },
  data() {
    return {
      itemText2: {
        nome: ''
      },
      metas: [{
          nome: 'Fazer um bolo de chocolate'
        },
        {
          nome: 'Aprender como gerir uma confeitaria'
        },
        {
          nome: 'Obter financiamento para a criação de um empreendimento'
        },
      ],
      itemText: {
        nome: ''
      }
    }
  },
  methods: {
    addItem: function() {
      var itemTextContent
      itemTextContent = this.itemText
      if (itemTextContent.nome == '') {
        return
      }
      this.metas.push(itemTextContent)
      this.itemText = {
        nome: ''
      }
    },
    // addItem: function() {
    //   var itemTextContent
    //   if(this.itemText.nome){
    //   console.log("Foco a")
    //   itemTextContent = this.itemText
    //   this.itemText2 = {nome: '', country:''};}
    //   if(this.itemText2.nome){
    //   console.log("Foco b")
    //   itemTextContent = this.itemText2}
    //   if(!itemTextContent){return;}
    //   this.metas.push(itemTextContent)
    //   this.itemText = {nome: '', country:''}
    // },
    removeItem: function(x) {
      this.metas.splice(x, 1);
      // console.log(String(x))
    },
    changeItem: function(x) {
      var itemTextContent2
      itemTextContent2 = this.itemText2
      if (!itemTextContent2) {
        return;
      }
      this.metas.splice(x, 1, itemTextContent2);
      // this.itemText2 = {nome: '', country:''}
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
