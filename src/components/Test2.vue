<template>
<div>
  <h1>Vue Top Artist Countries</h1>
  <ul>
    <li v-for="(artist, x) in artists" :key="x" class="justify-content-between">
      <button v-b-modal="String(x)" class="btn btn-primary btn-sm">Expandir</button>
      <h3>{{x}} - {{artist.name}} from {{artist.country}}</h3>
      <button v-on:click="removeItem(x)" class="btn btn-primary btn-sm">x</button>
      <b-modal v-bind:id="String(x)" title="Descrição">
        <div class="">
          {{x}}. {{artist.name}} {{artist.country}} <br>
          <!-- {{msg.name}} <br> {{msg.country}} <br> -->
          <input class="input" type="text" v-model="itemText2.name" placeholder="Adicione um artista!">
          <input class="input" type="text" v-model="itemText2.country" placeholder="Adicione a cidade dele!" />
          <button class="button is-primary is-medium" @click="[changeMsg2(), changeItem(x)]">Editar!</button>
        </div>
      </b-modal>
    </li>
  </ul>
</div>
</template>
<script>
export default {
  name: 'Test2',
  data() {
    return {
    itemText2: {name: '', country: ''}
    }
  },
  props: {
    msg: Object,
    artists: Array,
  },
  methods: {
    changeMsg2() {
      this.$emit("changeMsg3", this.itemText2);
      console.log('message emit from child component');
      // this.$parent.addItem()
      this.itemText2 = {name: '', country:''};
    },
    removeItem: function(evt) {
      this.$parent.removeItem(evt);
    },
    changeItem: function(evt) {
      this.$parent.changeItem(evt);
      var itemTextContent2
      itemTextContent2 = this.itemText2
      if(!itemTextContent2){return;}
      this.itemText2 = {name: '', country:''}
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
