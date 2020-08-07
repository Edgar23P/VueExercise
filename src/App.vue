<template>
  <div id="app">
    <mycomponent msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import mycomponent from './components/mycomponent.vue'

export default {
  name: 'App',
  components: {
   mycomponent
  }
}
</script>

<style>

</style>
