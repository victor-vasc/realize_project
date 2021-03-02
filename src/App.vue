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
  <b-container>
    <div class="custom-navbar d-flex justify-content-center justify-content-sm-start">
      <b-nav tabs class="align-bottom d-flex align-items-end">
        <b-nav-item v-for="tab in tabs"
                    v-bind:key="tab.name"
                    v-bind:class="['tab-button', { active: currentTab.name === tab.name }]"
                    v-on:click="currentTab = tab"
                    class="mt-1 mb-2 mr-2 subtitle align-bottom "
                    variant="dark"
        >
          {{ tab.name }}
        </b-nav-item>
      </b-nav>
    </div>
    <keep-alive>
      <component :is="currentTab.component.component" v-bind="{...currentTab.component.props}" v-on="{...currentTab.component.methods}" class="tab"></component>
    </keep-alive>
  </b-container>
  <!-- <Test2 v-bind:metas="metas" v-on:changeMsg3="setMessage" :msg="itemText2" /> -->
</div>
</template>
<script>
// import Test from './components/Test.vue'
import Test2 from './components/Test2'
import Navbar from './components/Navbar'
import HelloWorld2 from './components/HelloWorld2'
import HelloWorld from './components/HelloWorld'

var metas = [{
          nome: 'Fazer um bolo de chocolate'
        },
        {
          nome: 'Aprender como gerir uma confeitaria'
        },
        {
          nome: 'Obter financiamento para a criação de um empreendimento'
        },
      ];
var itemText2 = {
        nome: ''
      }
function setMessage(msg){
      itemText2 = msg;
      console.log('MEU DEUS FUNCIONA CARALHO', msg)
    }
var tabs = [{
    name: "Dashboard",
    component: { component: Test2, props: {metas: metas, msg: itemText2}, methods: {changeMsg3: setMessage}},
  },
  {
    name: "Resultado da busca",
    component:  { component: HelloWorld2, props: {msg: "TESTE"}},
  },
];
export default {
  nome: 'app',
  components: {
    // Test,
    Test2,
    Navbar,
    HelloWorld2
  },
  data() {
    return {
      tabs: tabs,
      metas: metas,
      currentTab: tabs[0],
      itemText2: itemText2,
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
    setMessage: setMessage
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
