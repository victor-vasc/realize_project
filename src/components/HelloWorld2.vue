<template>
  <div class="metas">
    <Navbar/>
    
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
.metasModalButton{
   height: 15vh;
 }
 .metaProgresso{
   transform:rotate(-90deg);
   width: 80vh;
 }
 .metaProgresso .progress{
   width: 660px;
    /* display: flex; */
    position: absolute;
    bottom: 0px;
    left: 20px;
 }
</style>
