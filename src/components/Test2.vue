<template>
<div>

  <Navbar />
    <b-modal class="novaMetaModal" centered id="modal-1">
      <template #modal-title>
        Adicionar nova meta
      </template>
        <div class="text-start">
          <h3 class="mb-3">Metas:</h3>
          <b-form>
            <b-form-group
              id="input-group-1"
              label="Definição da meta:"
              label-for="input-1"
              description="Insira o nome da meta desejada nesse campo."
              class="mx-0"
            >
              <b-form-input
                id="input-1"
                v-model="meta.nome"
                type="text"
                placeholder="Insira sua meta!"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group
              id="input-group-2"
              label="Descrição da meta:"
              label-for="input-2"
              class="mx-0"
              >
              <b-form-textarea
                id="input-2"
                v-model="meta.descricao"
                type="text"
                placeholder="Descrição de sua meta..."
                rows="3"
                max-rows="6"
                optional
              ></b-form-textarea>
            </b-form-group>

            <b-card class="metaSecCard border-left-0 border-right-0 border-bottom-0 rounded-0">
            <h3 class="mb-3">Metas secundárias:</h3>
            <b-card class="mb-2" v-for="(item, x) in meta.metaSecundaria" :key="x" header-tag="header">
              <template #header>
                <div class="d-flex align-items-center justify-content-between">
                  <h6 class="mb-0 d-inline-block">{{meta.metaSecundaria[x].nome}}</h6>
                  <h6 class="mb-0 d-inline-block text-right" @click="deleteMetaSecundaria(x)" ><b-icon font-scale="1.6" icon="x" text="dark" aria-label="Remove"></b-icon></h6>
                </div>
              </template>
                <h6>{{meta.metaSecundaria[x].descricao}}</h6>
              </b-card>
            <b-form-group
              id="input-group-1"
              label="Definição das metas secundários"
              label-for="input-1"
              description="Insira a definição de suas metas secundárias!"
              class="mx-0"
            >
              <b-form-input
                id="input-1"
                v-model="metaSecundariaConteudo.nome"
                type="text"
                placeholder="Insira sua meta secundária!"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group
              id="input-group-2"
              label="Descrição da meta secundária:"
              label-for="input-2"
              class="mx-0"
              >
              <b-form-textarea
                id="input-2"
                v-model="metaSecundariaConteudo.descricao"
                type="text"
                placeholder="Descrição da meta secundária..."
                rows="3"
                max-rows="6"
                optional
              ></b-form-textarea>
            </b-form-group>
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

  <b-list-group>
    <b-list-group-item v-for="(meta, x) in metas" :key="x" class="justify-content-between">
      <div>
        <b-card no-body class="overflow-hidden" v-b-modal="String(x)" style="max-width: 540px;">
          <b-row no-gutters>
            <b-col md="6">
              <!-- <b-card-img src="https://picsum.photos/400/400/?image=20" alt="Image" class="rounded-0"></b-card-img> -->
            </b-col>
            <b-col md="6">
              <b-card-body v-bind:title="meta.nome">
                <!-- <b-card-text>
                  This is a wider card with supporting text as a natural lead-in to additional content.
                  This content is a little bit longer.
                </b-card-text> -->

                <b-modal centered v-bind:id="String(x)" title="Descrição">
                  <template #modal-header="{ close }">
                    <!-- Emulate built in modal header close button action -->
                    <h5>Descrição</h5>
                      <b-icon font-scale="1.6" icon="trash" text="dark" aria-label="Remove" v-on:click="removeItem(x), close()"></b-icon>
                  </template>

                    <p><b>Meta</b><br>{{meta.nome}}</p>
                    <p><b>Descrição</b><br>{{meta.descricao}}</p>
                  <hr>
                    <div class="" v-for="item, x in meta.metaSecundaria" :key="x">
                      <p><b>Meta secundária</b></p>
                      <p>{{meta.metaSecundaria[x].nome}}</p>
                      <p><b>Descrição</b></p>
                    <p>{{meta.metaSecundaria[x].descricao}}</p>
                    <hr>
                    </div>

                </b-modal>
              </b-card-body>
            </b-col>
          </b-row>
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
      itemText2: {
        nome: '',
        descricao: '',
      },
      metaSecundariaConteudo:{
        nome:'',
        descricao:'',
      },
      // adicionar metaSecundaria um Array para conter multiplos objetos de metas secundárias
      meta: {
        nome: '',
        descricao: '',
        metaSecundaria:[]
      },
    }
  },
  props: {
    metas: Array,
  },
  methods: {
    metaSecNome: function(){
    },
    metaSecDescricao: function(){
    },

    addMetaSecundaria: function(){
      var itemMetaSecundaria
      itemMetaSecundaria = this.metaSecundariaConteudo
      if (itemMetaSecundaria.nome == '') {
        return
      }
      if(itemMetaSecundaria.descricao == ''){
        this.metaSecundariaConteudo.descricao = "nenhum conteúdo foi adicionado..."
      }
      this.meta.metaSecundaria.push(itemMetaSecundaria)
      this.metaSecundariaConteudo = {
        nome:'',
        descricao:'',
      }
      console.log(itemMetaSecundaria)
    },

    changeMsg2() {
      this.$emit("changeMsg3", this.itemText2);
      console.log('message emit from child component');
      this.itemText2 = {
        nome: ''
      }
    },
    addItem: function(){
      console.log(this.meta.nome);
      this.$emit("changeMsg3", this.meta);
      this.$parent.addItem()
      this.meta = {
        nome: '',
        descricao: '',
        metaSecundaria:[]
      }
    },
    removeItem: function(evt) {
      this.$parent.removeItem(evt);
    },
    deleteMetaSecundaria: function(x){
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
      console.log(evt)
    },
  }
}
</script>
<style scoped>
</style>
