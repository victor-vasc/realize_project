<template>
<div class="metas">
  <Navbar :navbarButtonIcon="navbarButton"/>
  <b-container class="p-0">
    <b-row>
      <div>
        <b-card :title="msg[x].nome" img-src="../assets/Logo Grupo 6 fundo branco.png" img-alt="Image" img-top tag="article" class="mb-2 shadow-sm ">
          <b-card-text>
            {{msg[x].descricao}}
          </b-card-text>

          <!-- <b-button href="#" variant="primary">Go somewhere</b-button> -->
        </b-card>
      </div>
    </b-row>
    <h4 class="mt-3 mb-3 pl-2">Metas secundárias:</h4>
    <b-row align-v="end">
      <b-col cols="12" class="p-0 mb-5">

        <div v-for="metaSecundaria, index in msg[x].metaSecundaria" :key="index" class="accordion mb-3" role="tablist">
          <b-card no-body class="mb-2 border-0">
            <b-card-header header-tag="header" class="shadow-sm mb-2 pl-3 mr-5 metaModalButton" :class="{metaSecundariaActive: index < 1 + msg[x].metasCompletadas.length && index == msg[x].metasCompletadas.length}" role="tab" header-bg-variant="info" header-text-variant="white">
              <div class="text-left metaHeader">
                <b-row align-v="center">
                  <b-col cols="1" class="pl-4">
                    <b-form-checkbox size="lg"
                      :value="index"
                      :disabled="index >= 1 + msg[x].metasCompletadas.length ||
                                 msg[x].metasCompletadas.indexOf(index) != -1"
                      v-model="msg[x].metasCompletadas[index]"
                      class="d-inline-block"
                      style="transform:scale(1.3)">
                      <!-- {{msg[x].metasCompletadas[index] == null || msg[x].metasCompletadas[index] === false ? "NAO" : "SIM"}} -->
                    </b-form-checkbox>
                    <!-- :disabled="index >= 1 + metasSelecionadas.length ||
                              metasSelecionadas.length <= metasSelecionadas.length + 1 &&
                              metasSelecionadas.indexOf(index) != -1"  -->                  </b-col>
                  <b-col cols="8" class="text-nowrap text-truncate d-inline-block pl-4">
                    <b>{{index + 1}}</b>. {{msg[x].metaSecundaria[index].nome}}
                  </b-col>
                  <b-col cols="2" class="px-3 text-right" v-b-modal="'modalMetasSecundárias-' + index">
                    <!-- action para expandir o accordeon component -->
                    <!--  v-b-toggle="'accordion-' + index" -->
                    <b-icon class="" font-scale="1" icon="arrow-up-right" text="dark" aria-label="Remove"></b-icon>
                  </b-col>
                </b-row>
              </div>
            </b-card-header>
            <b-collapse id="accordion" :accordion="'my-accordion' + index" role="tabpanel">
              <b-card class="pb-0">

              <b-card-body class="p-0">
                    <b-card-title>{{index + 1}}. Meta:</b-card-title>
                  <b-card-text class="">{{msg[x].metaSecundaria[index].nome}}</b-card-text>
                    <hr class="my-3">
                    <b-card-title>Descrição da meta:</b-card-title>
                  <b-card-text class="">{{msg[x].metaSecundaria[index].descricao}}</b-card-text>
                </b-card-body>

                <hr class="my-3">

                <b-card>
                  <b-card-title>Tarefas:</b-card-title>
                  <b-card-text>
                    <b-form-group label-size="mg" v-slot="{ tarefasMeta }">
                      <b-form-checkbox v-for="item in msg[x].metaSecundaria[index].options" v-model="msg[x].metaSecundaria[index].selected" :key="msg[x].metaSecundaria[index].nome + item.tarefa" :value="msg[x].metaSecundaria[index].nome + item.tarefa"
                        :aria-describedby="tarefasMeta" name="tarefas" class="ml-3">
                        {{item.tarefa}}
                      </b-form-checkbox>
                    </b-form-group>
                  </b-card-text>
                </b-card>

              </b-card>
            </b-collapse>
          </b-card>
          <div class="">
            <b-modal :id="'modalMetasSecundárias-' + index" centered hide-footer title-class="text-nowrap text-truncate w-100">
              <template #modal-title>
                <h5 class="text-truncate m-0 w-75">Descrição:</h5>
              </template>

                <b-card-body class="p-0">
                  <b-card-title>{{index + 1}}. Meta:</b-card-title>
                <b-card-text class="">{{msg[x].metaSecundaria[index].nome}}</b-card-text>
                  <hr class="my-3">
                  <b-card-title>Descrição da meta:</b-card-title>
                <b-card-text class="">{{msg[x].metaSecundaria[index].descricao}}</b-card-text>
                  <!-- <hr> -->
                  <b-card class="shadow-sm">
                    <b-card-title>Tarefas:</b-card-title>
                    <b-card-text>
                      <b-form-group size="mg" v-slot="{ tarefasMeta }">
                        <b-form-checkbox v-for="item in msg[x].metaSecundaria[index].options" v-model="msg[x].metaSecundaria[index].selected" :key="msg[x].metaSecundaria[index].nome + item.tarefa" :value="msg[x].metaSecundaria[index].nome + item.tarefa"
                          :aria-describedby="tarefasMeta" name="tarefas" class="">
                          {{item.tarefa}}
                        </b-form-checkbox>

                      </b-form-group>
                    </b-card-text>
                  </b-card>
                </b-card-body>

              <template #modal-footer="{close}">
                <b-button size="sm" variant="secondary" @click="close()">
                  Fechar
                </b-button>
              </template>
            </b-modal>
          </div>
        </div>

      </b-col>
    </b-row>
  </b-container>
</div>
</template>

<script>
import Navbar from './Navbar'

export default {
  name: 'Metas',
  components: {
    Navbar
  },
  props: {
    msg: Array,
    x: Number,
    navbarButton: String,
    metasSelecionadas: Array,
  },
  data() {
    return {
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.metaModalButton{
  border-top-right-radius: 2em!important;
  border-bottom-right-radius: 2em!important;
  border-top-left-radius: 0!important;
  border-bottom-left-radius: 0!important;
}
.metaSecundariaActive{
  background-color: var(--info)!important;
  font-weight: 600!important;
  padding-top: 1.5rem!important;
  padding-bottom: 1.5rem!important;
  border-top-right-radius: 3em!important;
  border-bottom-right-radius: 3em!important;
  /* margin-top: 1.5rem!important;
  margin-bottom: 1.5rem!important; */
  margin-right: 1rem!important;
}
</style>
