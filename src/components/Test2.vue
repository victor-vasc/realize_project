<template>
<div>
  <!-- <h1>Metas</h1> -->
  <Navbar />
    <b-modal centered id="modal-1">
      <template #modal-title>
        Adicionar nova meta
      </template>
        <div>
          <b-form>
            <b-form-group
              id="input-group-1"
              label="Definição da meta:"
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
              label-for="input-2"
              >
              <b-form-textarea
                id="input-2"
                v-model="meta.descricao"
                placeholder="Descrição de sua meta..."
                rows="3"
                max-rows="6"
                optional
              ></b-form-textarea>
            </b-form-group>

            <hr>
            <b-card>
            <b-form-group
              id="input-group-1"
              label="Definição das metas secundários"
              label-for="input-1"
              description="Insira a definição de suas metas secundárias!"
            >
              <b-form-input
                id="input-1"
                v-model="meta.metaSec.nome"
                type="text"
                placeholder="Insira sua meta secundária!"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group
              id="input-group-2"
              label="Descrição da meta secundária:"
              label-for="input-2"
              >
              <b-form-textarea
                id="input-2"
                v-model="meta.metaSec.descricao"
                placeholder="Descrição da meta secundária..."
                rows="3"
                max-rows="6"
                optional
              ></b-form-textarea>
            </b-form-group>
            <b-button class="float-right" type="submit" variant="primary">Adicionar</b-button>
          </b-card>
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

            <!-- <b-button type="submit" variant="primary">Submit</b-button>
            <b-button type="reset" variant="danger">Reset</b-button> -->
          </b-form>

          <b-card class="mt-3" header="Form Data Result">
            <pre class="m-0">{{ meta }}</pre>
          </b-card>
        </div>

      <template #modal-footer="{ ok, cancel}">
        <b-button type="submit" size="sm" variant="primary" @click="ok(), addItem()">
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

                <b-modal centered v-bind:id="String(x)" title="Descrição">
                  <template #modal-header="{ close }">
                    <!-- Emulate built in modal header close button action -->
                    <h5>Descrição</h5>
                      <b-icon font-scale="1.6" icon="trash" text="dark" aria-label="Remove" v-on:click="removeItem(x), close()"></b-icon>
                  </template>
                  <div class="" v-for="(metaSec, index) in meta" :key="index">
                    {{metaSec.nome}}
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
        metaSec:{
          nome:'',
          descricao: '',
        }
      },
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
