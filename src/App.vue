<template>
  <div id="app">
    <Weatherbox/>
    <Header/>
    
    
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Weatherbox from "./components/Weatherbox.vue"


export default {
  name: "App",
  components: {
    Weatherbox, 
    Header
    
  },
};
</script>

<style>

</style>
