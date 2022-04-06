<template>
  <div id="app">
    <HelloWorld/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style lang="sass">
*
  margin: 0
  padding: 0
  box-sizing: border-box
  font-family: serif

body
  display: flex 
  height: 100vh 
  justify-content: center
  align-items: center
  padding: 10px
  background: #cdcdcd

</style>
