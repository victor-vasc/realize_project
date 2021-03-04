<template>
<div>
  <!-- <h1>Metas</h1> -->
  <Navbar />
    <b-modal centered id="modal-1">
      <template #modal-title>
        Adicionar nova meta
      </template>
      <b-container>
        <div>
          <b-form @submit="onSubmit" @reset="onReset" v-if="show">
            <b-form-group
              id="input-group-1"
              label="Nome da meta:"
              label-for="input-1"
              description="Insira o nome da meta desejada nesse campo."
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
              label-for="input-2">
              <!-- <b-form-input
                id="input-2"
                v-model="form.name"
                placeholder="Enter name"
                required
              ></b-form-input> -->
              <b-form-textarea
                id="input-2"
                v-model="meta.descricao"
                placeholder="Insira a descrição de sua meta..."
                rows="3"
                max-rows="6"
                optional
              ></b-form-textarea>
            </b-form-group>

            <!-- <b-form-group id="input-group-3" label="Food:" label-for="input-3">
              <b-form-select
                id="input-3"
                v-model="form.food"
                :options="foods"
                required
              ></b-form-select>
            </b-form-group> -->

            <!-- <b-form-group id="input-group-4" v-slot="{ ariaDescribedby }">
              <b-form-checkbox-group
                v-model="form.checked"
                id="checkboxes-4"
                :aria-describedby="ariaDescribedby"
              >
                <b-form-checkbox value="me">Check me out</b-form-checkbox>
                <b-form-checkbox value="that">Check that out</b-form-checkbox>
              </b-form-checkbox-group>
            </b-form-group> -->

            <b-button type="submit" variant="primary">Submit</b-button>
            <b-button type="reset" variant="danger">Reset</b-button>
          </b-form>

          <b-card class="mt-3" header="Form Data Result">
            <pre class="m-0">{{ meta }}</pre>
          </b-card>
        </div>
      </b-container>

      <template #modal-footer="{ ok, cancel}">
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
                <b-modal centered v-bind:id="String(x)" title="Descrição">
                  <template #modal-header="{ close }">
                    <!-- Emulate built in modal header close button action -->
                    <h5>Descrição</h5>
                      <b-icon font-scale="1.6" icon="trash" text="dark" aria-label="Remove" v-on:click="removeItem(x), close()"></b-icon>
                  </template>
                  <div class="">
                    {{meta.nome}}<br>
                    {{meta.descricao}}
                    <!-- <b-form-input class="input" type="text" v-model="itemText2.nome" v-bind:placeholder="meta.nome"></b-form-input> -->
                    <!-- <b-button variant="primary" class="button is-primary is-medium" @click="[changeMsg2(), changeItem(x)]">Confirmar!</b-button> -->
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
      meta: {
        nome: '',
        descricao: '',
        food: null,
        checked: []
      },
      foods: [{ text: 'Select One', value: null }, 'Carrots', 'Beans', 'Tomatoes', 'Corn'],
      show: true
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
      console.log(this.meta.nome);
      this.$emit("changeMsg3", this.meta);
      this.$parent.addItem()
      this.meta = {
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
    },
    onSubmit(event) {
      event.preventDefault()
      alert(JSON.stringify(this.meta))
    },
    onReset(event) {
      event.preventDefault()
      // Reset our form values
      this.meta.nome = ''
      this.meta.descricao = ''
      this.meta.food = null
      this.meta.checked = []
      // Trick to reset/clear native browser form validation state
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
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
