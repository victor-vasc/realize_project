<template>
  <div class="metas">
    <Navbar/>
    <b-container class="pl-0">
      <b-row align-v="end">
        <b-col cols="12" class="pl-0">
          <div v-for="metaSecundaria, index in msg[x].metaSecundaria" :key="index" class="accordion" role="tablist">
            <b-card no-body class="mb-1 border-0">
              <b-card-header header-tag="header" class="p-0 border-0" role="tab">
                <b-button block v-b-toggle="'accordion-' + index" variant="primary" class="text-left metaHeader">
                  <b-row align-v="center">
                    <b-col cols="2">
                      <b-form-checkbox size="lg" class="d-inline-block"></b-form-checkbox>
                    </b-col>
                    <b-col cols="10">
                      {{msg[x].metaSecundaria[index].nome}}
                    </b-col>
                  </b-row>
                </b-button>
              </b-card-header>
              <b-collapse :id="'accordion-' + index" visible :accordion="'my-accordion' + index" role="tabpanel">
                <b-card-body>
                  <b-card-text>
                    <h5><b>Meta:</b></h5>
                    <p>{{msg[x].metaSecundaria[index].descricao}}</p>
                  </b-card-text>
                  <b-card-text>
                    <b-form-group
                      label="Tarefas:"
                      label-size="lg"
                      v-slot="{ tarefasMeta }"
                    >
                      <b-form-checkbox
                        v-for="item in msg[x].metaSecundaria[index].options"
                        v-model="msg[x].metaSecundaria[index].selected"
                        :key="msg[x].metaSecundaria[index].nome + item.tarefa"
                        :value="msg[x].metaSecundaria[index].nome + item.tarefa"
                        :aria-describedby="tarefasMeta"
                        name="tarefas"
                      >
                        {{item.tarefa}}
                      </b-form-checkbox>
                    </b-form-group>
                  </b-card-text>
                </b-card-body>
              </b-collapse>
            </b-card>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Navbar from './Navbar'

export default {
  name: 'HelloWorld',
  components: {
    Navbar
  },
  props: {
    msg: Array,
    x: Number,
  },
  data() {
      return {
        selected: [], // Must be an array reference!
        options: [
          { text: 'Fazer um bolo', value: 'orange' },
          { text: 'Pesquisar receitas', value: 'apple' },
          { text: 'Comprar Ingredientes', value: 'pineapple' },
          { text: 'Assar o bolo', value: 'grape' }
        ],
        value: 33.333333333,
        max: 50
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.accordion button{
  border-top-right-radius: 15px;
  border-bottom-right-radius: 15px;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
/* .metaHeader label.custom-control-label{
  overflow: hidden!important;
  text-overflow: ellipsis!important;
  white-space: nowrap!important;
  max-width: 150px!important;
} */
input[type="checkbox"]:checked ~ label {
    color: green;
}
 .progressBar{
   background-color: red;
   height: 100%;
  /* transform: rotate(-90deg);
  transform-origin: right top;
  -ms-transform: rotate(-90deg);
  -ms-transform-origin:right top;
  -webkit-transform: rotate(-90deg);
  -webkit-transform-origin:right top */
}/*
.progress{
  width: 100vh;
  position:relative;
  left:20px;
  top:-20px;
} */
</style>
