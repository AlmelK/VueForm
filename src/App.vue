<template>
  <div id="app">
    <VueForm/>
  </div>
</template>

<script>
import VueForm from './components/VueForm.vue'

export default {
  name: 'App',
  components: {
    VueForm
  }
}
</script>

<style lang="sass">
@import url('https://fonts.googleapis.com/css2?family=Alegreya+Sans:wght@300&family=Montserrat:wght@300;400;500;600;700&display=swap')

*
  margin: 0
  padding: 0
  box-sizing: border-box
  font-family: 'Montserrat', sans-serif

body
  display: block  
  height: 100%   
  padding: 10px
  background: linear-gradient(to left, #ccc, #ccc 20%, #fff 100%)

</style>
