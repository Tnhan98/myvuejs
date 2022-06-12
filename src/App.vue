<template>
  <Header />
  <Todos />
</template>

<script>
import Header from './components/Header.vue'
import Todos from './components/Todos.vue'
export default {
  name: 'App',
  components: {Header, Todos}
}
</script>

<style>
*{
  padding: 0;
  margin: 0;
}
</style>
