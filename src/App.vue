<template>
<div id="app">
  <b-container style="margin: 86px 0">
    <keep-alive>
      <component :is="currentTab.component.principal" v-bind="{...currentTab.component.props}" v-on:changeMsg3="setMessage" v-on:changeTab="changeTab" :x="tabSelecionada" class="tab"></component>
    </keep-alive>
    <b-navbar fixed="bottom" toggleable="lg" variant="info">
      <b-nav class="border-0 w-100 justify-content-between">
        <b-nav-item style="max-heignt: 56px" class="m-0" type="dark"
          v-for="tab in tabs"
          v-bind:key="tab.name"
          v-bind:class="['tab-button', { active: currentTab.name === tab.name }]"
          v-on:click="currentTab = tab"
        >
          <h5 class="mb-1 text-center"><b-icon style="width: 21px; height: 21px;" :icon="tab.tabIcon"></b-icon></h5>
          <h6 class="mb-0" style="font-size: 0.85em">{{ tab.name }}</h6>
        </b-nav-item>
      </b-nav>
    </b-navbar>
  </b-container>
  <!-- <Test2 v-bind:metas="metas" v-on:changeMsg3="setMessage" :msg="itemText2" /> -->
</div>
</template>
<script>
// import Test from './components/Test.vue'
import Test2 from './components/Test2'
import HelloWorld2 from './components/HelloWorld2'
import HelloWorld from './components/HelloWorld'

var metas = [
         {nome: 'Fazer um bolo de chocolate',
          descricao: 'É muito gostoso!',
          metaSecundaria:[{
            nome:'teste1',
            descricao: 'teste1',
            selected: [], // Must be an array reference!
            options: [
               { tarefa: 'Orange'},
               { tarefa: 'Apple'},
               { tarefa: 'Pineapple' },
               { tarefa: 'Grape' },
             ],
          }]
        },{nome: 'Fazer um bolo de c2222222222hocolate',
         descricao: 'É muito gostoso!',
         metaSecundaria:[{
           nome:'teste1',
           descricao: 'teste1',
           selected: [], // Must be an array reference!
           options: [
              { tarefa: 'Orange'},
              { tarefa: 'Apple'},
              { tarefa: 'Pineapple' },
              { tarefa: 'Grape' },
            ],
         }]
       },{nome: 'Fazer um bolo de c333333333333hocolate',
        descricao: 'É muito gostoso!',
        metaSecundaria:[{
          nome:'teste1',
          descricao: 'teste1',
          selected: [], // Must be an array reference!
          options: [
             { tarefa: 'Orange'},
             { tarefa: 'Apple'},
             { tarefa: 'Pineapple' },
             { tarefa: 'Grape' },
           ],
        }]
      },
      ];
var itemText2;
var itemText;
var tabs = [{
    name: "Home",
    tabIcon: "house-door-fill",
    component: { principal: Test2, props: {metas: metas, msg:itemText2}},
  },
  {
    name: "Metas",
    tabIcon: "list-ul",
    component:  { principal: HelloWorld2, props: {msg: metas}},
  },
  {
    name: "Contato",
    tabIcon: "chat-left-text-fill",
    component:  { principal: HelloWorld, props: {msg: "Contato Página"}},
  }
];
export default {
  nome: 'app',
  components: {
    // Test,
    Test2,
    HelloWorld2
  },
  data() {
    return {
      tabs: tabs,
      metas: metas,
      currentTab: tabs[0],
      itemText2: itemText2,
      itemText: itemText,
      tabSelecionada: '',
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
    },
    changeItem: function(x) {
      var itemTextContent2
      itemTextContent2 = this.itemText2
      if (!itemTextContent2) {
        return;
      }
      this.metas.splice(x, 1, itemTextContent2);
    },
    setMessage: function(msg) {
      this.itemText2 = msg;
      this.itemText = msg;
    },
    changeTab: function(evt){
      this.tabSelecionada = evt;
      console.log("teste", evt, this.tabSelecionada)
    }
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
.tab-button > a{
  color:rgba(255,255,255,0.7);
  padding-bottom: 0;
  padding-top: 0;

}
.active > a{
  color:white;
}
.metaSecCard > .card-body{
  padding:1em 0 0 0;
}
.modal-dialog-centered .modal-content  {
    margin: 60px 0;
}
.cardMetaBody{
  max-height: calc(70vh - 30px);
  overflow-y: auto;
}
</style>
