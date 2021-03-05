<template>
     <div class="hello">
       <h1 class="is-size-3">{{msg}}</h1>
     </div>
   </template>

   <script>
   /* eslint-disable */
   export default {
     name: "HelloWorld",
     data() {
       return {
       welcomeMsg: ""
       }
     },
     props: {
       msg: String
     },
     methods: {
       changeMsg2() {
         this.$emit("changeMsg3", this.welcomeMsg);
         console.log('message emit from child component')
       }
     }
   };
   </script>
   <!-- Add "scoped" attribute to limit CSS to this component only -->
   <style scoped>
   h3 {
     margin: 40px 0 0;
   }
   ul {
     list-style-type: none;
     padding: 0;
   }
   li {
     display: inline-block;
     margin: 0 10px;
   }
   a {
     color: #42b983;
   }
   </style>
