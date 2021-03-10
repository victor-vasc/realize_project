<template>
<div>

  <Navbar />
  <!-- inicio modal de nova meta -->
  <b-modal class="novaMetaModal" centered id="modal-1">
    <template #modal-title>
      Adicionar nova meta
    </template>
    <div class="text-start">
      <h3 class="mb-3">Metas:</h3>
      <b-form>
        <b-form-group id="input-group-1" label="Definição da meta:" label-for="input-1" description="Insira o nome da meta desejada nesse campo." class="mx-0">
          <b-form-input id="input-1" v-model="meta.nome" type="text" placeholder="Insira sua meta!" required></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Descrição da meta:" label-for="input-2" class="mx-0">
          <b-form-textarea id="input-2" v-model="meta.descricao" type="text" placeholder="Descrição de sua meta..." rows="3" max-rows="6" optional></b-form-textarea>
        </b-form-group>

        <b-card class="metaSecCard border-left-0 border-right-0 border-bottom-0 rounded-0">
          <h3 class="mb-3">Metas secundárias:</h3>
          <b-card class="mb-2" v-for="(item, x) in meta.metaSecundaria" :key="x" header-tag="header" no-body>
            <template #header>
              <div class="d-flex align-items-center justify-content-between">
                <h6 v-b-toggle="'accordion-' + x" class="mb-0 d-inline-block"><b>{{x}}.</b> {{meta.metaSecundaria[x].nome}}</h6>
                <h6 class="mb-0 d-inline-block text-right" @click="deleteMetaSecundaria(x)">
                  <b-icon font-scale="1.6" icon="x" text="dark" aria-label="Remove"></b-icon>
                </h6>
              </div>
            </template>
            <b-collapse :id="'accordion-' + x" visible accordion="my-accordion" role="tabpanel">
              <b-card-body>
                <h6>{{meta.metaSecundaria[x].descricao}}</h6>
                <!-- <h6>{{meta.metaSecundaria[x].options}}</h6> -->
                <b-form-group
                  label="Tarefas:"
                  label-size="lg"
                  v-slot="{ ariaDescribedby2 }"
                >
                  <b-form-checkbox
                    v-for="item in meta.metaSecundaria[x].options"
                    v-model="meta.metaSecundaria[x].selected"
                    :key="meta.metaSecundaria[x].nome + item.tarefa"
                    :value="meta.metaSecundaria[x].nome + item.tarefa"
                    :aria-describedby="ariaDescribedby2"
                    name="flavour-4a"
                  >
                    {{item.tarefa}}
                  </b-form-checkbox>
                </b-form-group>
              </b-card-body>
            </b-collapse>
          </b-card>
          <b-form-group id="input-group-1" label="Definição das metas secundários" label-for="input-1" description="Insira a definição de suas metas secundárias!" class="mx-0">
            <b-form-input id="input-1" v-model="metaSecundariaConteudo.nome" type="text" placeholder="Insira sua meta secundária!" required></b-form-input>
          </b-form-group>

          <b-form-group id="input-group-2" label="Descrição da meta secundária:" label-for="input-2" class="mx-0">
            <b-form-textarea id="input-2" v-model="metaSecundariaConteudo.descricao" type="text" placeholder="Descrição da meta secundária..." rows="3" max-rows="6" optional></b-form-textarea>
          </b-form-group>

          <b-form-group
            label="Tarefas:"
            label-size="lg"
            v-slot="{ TarefasCheck }"
            class="text-break"
          >
            <b-form-checkbox
              v-for="option in metaSecundariaConteudo.options"
              v-model="metaSecundariaConteudo.selected"
              :key="option.tarefa"
              :value="option.tarefa"
              :aria-describedby="TarefasCheck"
              name="TarefasCheck"
            >
              {{ option.tarefa }}
            </b-form-checkbox>
          </b-form-group>
          <div class="mb-3">
            <b-button class="d-inline" @click="addTarefa" size="sm" variant="link"><b-icon font-scale="1.6" icon="plus" text="dark" aria-label="Remove"></b-icon></b-button>
            <b-form-input class="d-inline w-75 align-middle border-top-0 border-left-0 border-right-0" v-model="novaTarefa.tarefa" placeholder="Adicionar nova meta..."></b-form-input>
          </div>
          <b-button class="float-right" @click="addMetaSecundaria" variant="primary">Adicionar</b-button>
        </b-card>
      </b-form>

      <!-- <b-card class="mt-3" header="Form Data Result">
            <pre class="m-0">{{ meta }}</pre>
          </b-card> -->
    </div>

    <template #modal-footer="{ ok, cancel}">
      <b-button type="submit" size="sm" variant="info" @click="ok(), addItem()">
        Adicionar
      </b-button>
      <b-button type="cancel" size="sm" variant="secondary" @click="cancel()">
        Cancelar
      </b-button>
    </template>
  </b-modal>

  <!-- final modal de nova meta -->

  <b-list-group>
    <b-list-group-item v-for="(meta, x) in metas" :key="x" class="justify-content-between border-0 px-0 pb-0">
      <div>
        <b-card
          no-body
          class="overflow-hidden mb-3"
          v-on:click="changeTab(x)"
          v-b-modal="String(x)"
          style="max-width: 540px;"
         >
         <!-- v-b-modal="String(x)" -->
              <b-card-body v-bind:title="meta.nome" class="bg-info text-light">
                <b-modal centered v-bind:id="String(x)" title="Descrição" body-class="cardMetaBody" footer-class="justify-content-start" >
                  <p><b>Meta</b><br>{{meta.nome}}</p>
                  <p><b>Descrição</b><br>{{meta.descricao}}</p>
                  <hr>
                  <div class="" v-for="item, x in meta.metaSecundaria" :key="x">
                    <p><b>Meta secundária {{x + 1}}</b></p>
                    <p>{{meta.metaSecundaria[x].nome}}</p>
                    <p><b>Descrição</b></p>
                    <p>{{meta.metaSecundaria[x].descricao}}</p>
                    <hr>
                    <b-form-group
                      label="Tarefas:"
                      label-size="lg"
                      v-slot="{ ariaDescribedby2 }"
                    >
                      <b-form-checkbox
                        v-for="item in meta.metaSecundaria[x].options"
                        v-model="meta.metaSecundaria[x].selected"
                        :key="meta.metaSecundaria[x].nome + item.tarefa"
                        :value="meta.metaSecundaria[x].nome + item.tarefa"
                        :aria-describedby="ariaDescribedby2"
                        name="flavour-4a"
                      >
                        {{item.tarefa}}
                      </b-form-checkbox>
                    </b-form-group>
                  </div>
                  <template #modal-footer="{cancel}">
                    <b-button type="cancel" size="mg" variant="danger" @click="removeItem(x), cancel()">
                      Deletar meta
                    </b-button>
                  </template>
                </b-modal>
              </b-card-body>
        </b-card>
      </div>
    </b-list-group-item>
  </b-list-group>
</div>
</template>
<script>
import Navbar from './Navbar'
export default {
  name: 'Test2',
  components: {
    // Test,
    Navbar,
  },
  data() {
    return {
      // itemText2: {
      //   nome: '',
      //   descricao: '',
      // },
      metaSelecionada:'',
      novaTarefa: [{tarefa:''}],
      metaSecundariaConteudo: {
        nome: '',
        descricao: '',
        selected: [], // Must be an array reference!
        options: [
         ],
      },
      meta: {
        nome: '',
        descricao: '',
        metaSecundaria: []
      },
    }
  },
  props: {
    metas: Array,
  },
  watch: {
    // metaSelecionada: function(){
    //
    // }
  },
  methods: {
    metaSecNome: function() {},
    metaSecDescricao: function() {},

    changeTab: function(x){
      // this.$parent.$data.currentTab = this.$parent.$data.tabs[1]
      this.$emit("changeTab", x);
    },

    addMetaSecundaria: function() {
      var itemMetaSecundaria
      itemMetaSecundaria = this.metaSecundariaConteudo
      if (itemMetaSecundaria.nome == '') {
        return
      }
      if (itemMetaSecundaria.descricao == '') {
        this.metaSecundariaConteudo.descricao = "nenhum conteúdo foi adicionado..."
      }
      this.meta.metaSecundaria.push(itemMetaSecundaria)
      this.metaSecundariaConteudo = {
        nome: '',
        descricao: '',
        selected: [], // Must be an array reference!
        options: [],
      }
    },
    addTarefa: function(){
      var metaTarefa
      metaTarefa = this.novaTarefa
      if (metaTarefa.tarefa == undefined){return}
      this.metaSecundariaConteudo.options.push(metaTarefa)
      this.novaTarefa = [{tarefa:''}]
      console.log(metaTarefa.tarefa)
    },

    changeMsg2() {
      this.$emit("changeMsg3", this.itemText2);
      this.itemText2 = {
        nome: ''
      }
    },
    addItem: function() {
      this.$emit("changeMsg3", this.meta);
      this.$parent.addItem()
      // this.meta = {
      //   nome: '',
      //   descricao: '',
      //   metaSecundaria: []
      // }
    },
    removeItem: function(evt) {
      this.$parent.removeItem(evt);
    },
    deleteMetaSecundaria: function(x) {
      this.meta.metaSecundaria.splice(x, 1);
    },
    changeItem: function(evt) {
      this.$parent.changeItem(evt);
      var itemTextContent2
      itemTextContent2 = this.itemText2
      if (!itemTextContent2) {
        return;
      }
      this.itemText2 = {
        nome: ''
      }
    },
  }
}
</script>
<style scoped>
</style>
