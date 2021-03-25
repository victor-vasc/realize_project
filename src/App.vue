Metas<template>
<div id="app">
  <b-container style="margin: 55px auto">
    <keep-alive>
      <component :is="currentTab.component.principal" v-bind="{...currentTab.component.props}" v-on:changeMsg3="setMessage" v-on:changeTab="changeTab" :navbarButton="currentTab.name" :x="tabSelecionada" :metasSelecionadas="metasSelecionadas" class="tab"></component>
    </keep-alive>
    <b-navbar fixed="bottom" toggleable="lg" variant="info" class="border-top border-light">
      <b-nav class="border-0 w-100 justify-content-around">
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
  <!-- <HomePage v-bind:metas="metas" v-on:changeMsg3="setMessage" :msg="itemText2" /> -->
</div>
</template>
<script>
// import Test from './components/Test.vue'
import HomePage from './components/HomePage'
import Metas from './components/Metas'
// import HelloWorld from './components/HelloWorld'

var metas = [
         {nome: 'Criar minha própria academia de jiu-jitsu',
          descricao: 'Atuar como professor é um sonho que eu possuo, pois quero poder me relacionar com pessoas com mesmo hobby. Agora que finalmente possuo algum tempo livre de meu trabalho, vou dar início ao meu projeto de vida',
          metasCompletadas: [],
          metaSecundaria:[{
            nome:'Aprender sobre gestão e planejamento de pequenos empreendimentos',
            descricao: 'O empreendedor deve buscar contínuo aperfeiçoamento das atividades necessárias para a excelência do negócio, buscando informações em cursos, eventos relacionados ao tema, mídia especializada no assunto ou junto a profissionais que atuam na área. Além dessas características básicas é fundamental que os profissionais dessa área tenham habilidades tanto técnicas quanto humanas, visando a correta receptividade de seus clientes.',
            selected: [], // Must be an array reference!
            options: [
               { tarefa: 'Procurar cursos e aulas sobre empreendedorismo'},
               { tarefa: 'Realizar um planejamento e modelo de negócio'},
               { tarefa: 'Aprender sobre gestão/gerenciamento'},
               { tarefa: 'Procurar por investimentos'},
             ],
          },
          {
            nome:' Pesquisa de locação e mercado',
            descricao: 'Para obter êxito na escolha do local, é importante, primeiramente, conhecer seu público alvo, pois além de influenciar na escolha do ponto comercial, faz parte do planejamento estratégico. O segundo passo é observar o fluxo de pessoas no local, tanto de pedestres quanto de carros. O próximo passo é avaliar a acessibilidade do ponto, ou seja, como chegar até o ponto comercial, a sua infraestrutura ao redor.',
            selected: [], // Must be an array reference!
            options: [
               { tarefa: 'Pesquisar possíveis imóveis para a academia'},
               { tarefa: 'Pesquisar sobre o público presente dentro daquela região' },
               { tarefa: 'Procurar por possíveis concorrentes após encontrar um imóvel'},
               { tarefa: 'Avaliar os custos em relação a alugar ou comprar' },
             ],
          },
          {
            nome:'Procurar por profissionais e equipamentos',
            descricao: 'Por mais que você se prepare para a abertura da empresa é bem provável que você se depare com um ambiente bem burocrático e complexo. Quanto mais você tentar encarar esse ambiente de maneira solitária, maior será a dor de cabeça. Sem contar que terá que contratar diversos serviços.',
            selected: [], // Must be an array reference!
            options: [
               { tarefa: 'Procurar por professores capacitados'},
               { tarefa: 'Procurar por profissinais de administração e contabilidade'},
               { tarefa: 'Procurar por uma equipe para realizar manutenções e limpeza dos equipamentos' },
             ],
          },
          {
            nome:'Procurar pelas documentações necessárias',
            descricao: 'Nenhuma descrição foi adicionada...',
            selected: [], // Must be an array reference!
            options: [],
          },
          {
            nome:'Marketing e divulgação',
            descricao: 'Os canais de distribuição são os meios pelos quais o empreendedor entrega o seu serviço ao cliente final, no local certo e na hora esperada pelos clientes. É a resposta às seguintes perguntas: Como o serviço chega ao cliente? Ou, de modo geral, qual a estratégia da empresa para que o cliente chegue à sua empresa?',
            selected: [], // Must be an array reference!
            options: [
               { tarefa: 'Contratar alguma empresa para realizar a divulgação da academia...'},
             ],
          }]
        },
      //   {nome: 'Fazer um bolo de c2222222222hocolate',
      //    descricao: 'É muito gostoso!',
      //    metaSecundaria:[{
      //      nome:'teste1',
      //      descricao: 'teste1',
      //      selected: [], // Must be an array reference!
      //      options: [
      //         { tarefa: 'Orange'},
      //         { tarefa: 'Apple'},
      //         { tarefa: 'Pineapple' },
      //         { tarefa: 'Grape' },
      //       ],
      //    }]
      //  },
      //  {nome: 'Fazer um bolo de c333333333333hocolate',
      //   descricao: 'É muito gostoso!',
      //   metaSecundaria:[{
      //     nome:'teste1',
      //     descricao: 'teste1',
      //     selected: [], // Must be an array reference!
      //     options: [
      //        { tarefa: 'Orange'},
      //        { tarefa: 'Apple'},
      //        { tarefa: 'Pineapple' },
      //        { tarefa: 'Grape' },
      //      ],
      //   }]
      // },
      ];
var itemText2;
var itemText;
var tabs = [{
    name: "Home",
    tabIcon: "house-door-fill",
    component: { principal: HomePage, props: {metas: metas, msg:itemText2}},
  },
  {
    name: "Metas",
    tabIcon: "list-ul",
    component:  { principal: Metas, props: {msg: metas}},
  },
  // {
  //   name: "Contato",
  //   tabIcon: "chat-left-text-fill",
  //   component:  { principal: HelloWorld, props: {msg: "Contato Página"}},
  // }
];
export default {
  nome: 'app',
  components: {
    // Test,
    HomePage,
    Metas
  },
  data() {
    return {
      tabs: tabs,
      metas: metas,
      currentTab: tabs[0],
      itemText2: itemText2,
      itemText: itemText,
      tabSelecionada: 0,
      metasSelecionadas: [],
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
/* .cardMetaBody{
  max-height: calc(70vh - 30px);
  overflow-y: auto;
} */
.custom-control-input:checked~.custom-control-label::before, .custom-checkbox .custom-control-input:disabled:checked~.custom-control-label::before{
  background-color: var(--info);
  border-color: var(--info);
}
.custom-control-input:focus~.custom-control-label::before{
  box-shadow:none
}
.metaHeader .custom-control-label::before{
  border-color: var(--info);
}
</style>
