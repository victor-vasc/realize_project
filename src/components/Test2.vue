<template>
<div>
  <!-- <h1>Metas</h1> -->
  <Navbar />
    <b-modal centered id="modal-1">
      <template #modal-title>
        Adicionar nova meta
      </template>
      <!-- <template #default="{ ok }">
        <p class="my  -4">
          <b-input input type="text" v-model="itemText.nome" placeholder="Adicione um meta!"></b-input>
          <b-button v-on:click="ok()" variant="primary" class="btn btn-primary btn-sm">Adicionar</b-button>
        </p>
      </template> -->
      <div class="">
        <h5>Nome da meta:</h5>
        <b-input input type="text" v-model="itemText.nome" placeholder="Adicione um meta!"></b-input>
      </div>
      <template #modal-footer="{ ok, cancel}">
        <!-- <b>Custom Footer</b> -->
        <!-- Emulate built in modal footer ok and cancel button actions -->
        <b-button size="sm" variant="primary" @click="ok(), addItem()">
          Adicionar
        </b-button>
        <b-button size="sm" variant="secondary" @click="cancel()">
          Cancelar
        </b-button>
      </template>
    </b-modal>
  <b-list-group>
    <b-list-group-item v-for="(meta, x) in metas" :key="x" class="justify-content-between">
      <div>
        <b-card no-body class="overflow-hidden" v-b-modal="String(x)"  style="max-width: 540px;">
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
                <!-- <b-button variant="primary" v-b-modal="String(x)" class="btn btn-primary btn-sm">Expandir</b-button> -->
                <b-modal v-bind:id="String(x)" title="Descrição">
                  <template #modal-header="{ close }">
                    <!-- Emulate built in modal header close button action -->
                    <h5>Descrição</h5>
                    <b-button variant="link" size="sm" v-on:click="removeItem(x); close()">
                      <b-icon v-b-modal.modal-1 font-scale="2" icon="x" aria-label="Add"></b-icon>
                    </b-button>
                  </template>
                  <div class="">
                    {{meta.nome}}<br>
                    <b-form-input class="input" type="text" v-model="itemText2.nome" v-bind:placeholder="meta.nome"></b-form-input>
                    <b-button variant="primary" class="button is-primary is-medium" @click="[changeMsg2(), changeItem(x)]">Confirmar!</b-button>
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
        nome: ''
      },
      itemText: {
        nome: ''
      }
    }
  },
  props: {
    metas: Array,
  },
  methods: {
    changeMsg2() {
      this.$emit("changeMsg3", this.itemText2);
      console.log('message emit from child component');
      this.itemText2 = {
        nome: ''
      }
    },
    addItem: function(){
      this.$emit("changeMsg3", this.itemText);
      this.$parent.addItem()
      this.itemText = {
        nome: ''
      }
    },
    removeItem: function(evt) {
      this.$parent.removeItem(evt);
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
    }
  }
}
</script>
<style scoped>
/* li {
  height: 40px;
  width: 100%;
  padding: 15px;
  border: 1px solid saddlebrown;
  display: flex;
  justify-content: center;
  align-items: center;
}

a {
  color: #42b983;
} */
</style>
