<template>
  <div id="app">
   
     <toDo />
  </div>

</template>

<script>

import toDo from './components/toDo';
export default {
  name: 'App',
  components: {
  
    toDo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: right;
  color: #1e81b0;
  margin-top: 100px;
  background-color: #e47144
  h1{
  font-text:bold;
  }

}
</style> 
