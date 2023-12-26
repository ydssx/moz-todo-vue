<template >
  <div id="app">
    <h1>To-do List</h1>
    <to-do-form @todo-added="addTodo"></to-do-form>
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <to-do-item :label="todo.label" :done="todo.done" :id="todo.id"></to-do-item>
      </li>
    </ul>
  </div>
</template>

<script>
import ToDoItem from './components/ToDoItem.vue';
import ToDoForm from './components/ToDoForm.vue';
import uniqueId from 'lodash.uniqueid';

export default {
  name: 'App',
  components: {
    ToDoItem,
    ToDoForm,
  },
  data() {
    return {
      todos: [
        { label: "Learn Vue", done: false, id: uniqueId("todo-item-") },
        { label: "Create a Vue project with the CLI", done: true, id: uniqueId("todo-item-") },
        { label: "Have fun", done: true, id: uniqueId("todo-item-") },
        { label: "Create a to-do list", done: false, id: uniqueId("todo-item-") },
      ],
    }
  },
  methods: {
    addTodo(label) {
      console.log("todo added");
      this.todos.push({ label, done: false, id: uniqueId("todo-item-") })
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id!== id)
    },
    toggleTodo(id) {
      this.todos = this.todos.map(todo => {
        if (todo.id === id) {
          return {...todo, done:!todo.done }
        }
        return todo
      })
    },
  },
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
