<template>
<div>
  <h1>Metas</h1>
  <ul>
    <li v-for="(meta, x) in metas" :key="x" class="justify-content-between">
      <button v-b-modal="String(x)" class="btn btn-primary btn-sm">Expandir</button>
      <h3>{{x}} - {{meta.nome}}</h3>
      <button v-on:click="removeItem(x)" class="btn btn-primary btn-sm">x</button>
      <b-modal v-bind:id="String(x)" title="Descrição">
        <div class="">
          {{x}}. {{meta.nome}}<br>
          <!-- {{msg.nome}} <br> {{msg.country}} <br> -->
          <input class="input" type="text" v-model="itemText2.nome" placeholder="Adicione um meta!">
          <!-- <input class="input" type="text" v-model="itemText2.country" placeholder="Adicione a cidade dele!" /> -->
          <button class="button is-primary is-medium" @click="[changeMsg2(), changeItem(x)]">Confirmar!</button>
        </div>
      </b-modal>
    </li>
  </ul>
</div>
</template>
<script>
export default {
  nome: 'Test2',
  data() {
    return {
    itemText2: {nome: ''}
    }
  },
  props: {
    msg: Object,
    metas: Array,
  },
  methods: {
    changeMsg2() {
      this.$emit("changeMsg3", this.itemText2);
      console.log('message emit from child component');
      // this.$parent.addItem()
      this.itemText2 = {nome: ''};
    },
    removeItem: function(evt) {
      this.$parent.removeItem(evt);
    },
    changeItem: function(evt) {
      this.$parent.changeItem(evt);
      var itemTextContent2
      itemTextContent2 = this.itemText2
      if(!itemTextContent2){return;}
      this.itemText2 = {nome: ''}
      console.log(evt)
    }
  }
}
</script>
<style scoped>
li {
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
}
</style>
