<template>
  <div class="metas">
    <Navbar/>
    <b-container class="p-0">
      <b-row>
        <div>
          <b-card
            :title="msg[x].nome"
            img-src="https://picsum.photos/600/300/?image=25"
            img-alt="Image"
            img-top
            tag="article"
            class="mb-2"
          >
            <b-card-text>
              {{msg[x].descricao}}
            </b-card-text>

            <!-- <b-button href="#" variant="primary">Go somewhere</b-button> -->
          </b-card>
        </div>
      </b-row>
      <h4 class="mt-5 mb-3 pl-2">Metas secundárias:</h4>
      <b-row align-v="end">
        <b-col cols="12" class="p-0 mb-5">
          <div v-for="metaSecundaria, index in msg[x].metaSecundaria" :key="index" class="accordion" role="tablist">
            <b-card no-body class="mb-2 border-0">
              <b-card-header header-tag="header" class="pl-3 border-0" role="tab" header-bg-variant="info" header-text-variant="white">
                <div class="text-left metaHeader">
                  <b-row align-v="center">
                    <b-col cols="1" class="pl-4">
                      <b-form-checkbox size="lg" class="d-inline-block" style="transform:scale(1.3)"></b-form-checkbox>
                    </b-col>
                    <b-col cols="8" class="text-nowrap text-truncate pl-4">
                      {{msg[x].metaSecundaria[index].nome}}
                    </b-col>
                    <b-col cols="2" class="px-3 text-right ml-auto">
                      <!-- action para expandir o accordeon component -->
                      <!--  v-b-toggle="'accordion-' + index" -->
                      <b-icon class="" font-scale="1.2" icon="box-arrow-in-up-right" text="dark" aria-label="Remove"></b-icon>
                    </b-col>
                  </b-row>
                </div>
              </b-card-header>
              <b-collapse :id="'accordion-' + index" :accordion="'my-accordion' + index" role="tabpanel">
                <b-card-body class="pb-0">
                  <b-card-text>
                    <h6><b>Descrição:</b></h6>
                    <p class="ml-3">{{msg[x].metaSecundaria[index].descricao}}</p>
                  </b-card-text>
                  <hr>
                  <b-card-text>
                    <b-form-group
                      label="Tarefas:"
                      label-size="mg"
                      v-slot="{ tarefasMeta }"
                    >
                      <b-form-checkbox
                        v-for="item in msg[x].metaSecundaria[index].options"
                        v-model="msg[x].metaSecundaria[index].selected"
                        :key="msg[x].metaSecundaria[index].nome + item.tarefa"
                        :value="msg[x].metaSecundaria[index].nome + item.tarefa"
                        :aria-describedby="tarefasMeta"
                        name="tarefas"
                        class="ml-3"
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
