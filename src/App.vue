<template >
  <div id="app"></div>
  <h1>To-do List</h1>
  <ul>
    <li><to-do-item label="Learn Vue.js"></to-do-item></li>
  </ul>
</template>

<script>
import ToDoItem from './components/ToDoItem.vue'
export default {
  name: 'App',
  components: {
    ToDoItem,
  }
}
</script>

<style >
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #1b24206b;
  margin-top: 60px;
}
</style>
