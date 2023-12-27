<template >
  <div id="app">
    <h1>To-do List</h1>
    <h2 id="list-summary">{{ listSummary }}</h2>
    <to-do-form @todo-added="addTodo"></to-do-form>
    <ul aria-labelledby="list-summary" class="stack-large">
      <li v-for="todo in todos" :key="todo.id">
        <to-do-item :label="todo.label" :done="todo.done" :id="todo.id"
          @checkbox-changed="updateTodo(todo.id)"></to-do-item>
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
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    toggleTodo(id) {
      this.todos = this.todos.map(todo => {
        if (todo.id === id) {
          return { ...todo, done: !todo.done }
        }
        return todo
      })
    },
    updateTodo(todoId) {
      const todoToUpdate = this.todos.find(todo => todo.id === todoId);
      todoToUpdate.done = !todoToUpdate.done;
    }
  },
  computed: {
    listSummary() {
      const done = this.todos.filter((todo) => todo.done).length;
      const total = this.todos.length;
      return `${done} of ${total} items done`;
    },
  },
}
</script>

<style>
/* 全局样式 */
.btn {
  padding: 0.8rem 1rem 0.7rem;
  border: 0.2rem solid #4d4d4d;
  cursor: pointer;
  text-transform: capitalize;
}

.btn__danger {
  color: #fff;
  background-color: #ca3c3c;
  border-color: #bd2130;
}

.btn__filter {
  border-color: lightgrey;
}

.btn__danger:focus {
  outline-color: #c82333;
}

.btn__primary {
  color: #fff;
  background-color: #000;
}

.btn-group {
  display: flex;
  justify-content: space-between;
}

.btn-group>* {
  flex: 1 1 auto;
}

.btn-group>*+* {
  margin-left: 0.8rem;
}

.label-wrapper {
  margin: 0;
  flex: 0 0 100%;
  text-align: center;
}

[class*="__lg"] {
  display: inline-block;
  width: 100%;
  font-size: 1.9rem;
}

[class*="__lg"]:not(:last-child) {
  margin-bottom: 1rem;
}

@media screen and (min-width: 620px) {
  [class*="__lg"] {
    font-size: 2.4rem;
  }
}

.visually-hidden {
  position: absolute;
  height: 1px;
  width: 1px;
  overflow: hidden;
  clip: rect(1px 1px 1px 1px);
  clip: rect(1px, 1px, 1px, 1px);
  clip-path: rect(1px, 1px, 1px, 1px);
  white-space: nowrap;
}

[class*="stack"]>* {
  margin-top: 0;
  margin-bottom: 0;
}

.stack-small>*+* {
  margin-top: 1.25rem;
}

.stack-large>*+* {
  margin-top: 2.5rem;
}

@media screen and (min-width: 550px) {
  .stack-small>*+* {
    margin-top: 1.4rem;
  }

  .stack-large>*+* {
    margin-top: 2.8rem;
  }
}

/* 全局样式结束 */
#app {
  background: #fff;
  margin: 2rem 0 4rem 0;
  padding: 1rem;
  padding-top: 0;
  position: relative;
  box-shadow:
    0 2px 4px 0 rgba(0, 0, 0, 0.2),
    0 2.5rem 5rem 0 rgba(0, 0, 0, 0.1);
}

@media screen and (min-width: 550px) {
  #app {
    padding: 4rem;
  }
}

#app>* {
  max-width: 50rem;
  margin-left: auto;
  margin-right: auto;
}

#app>form {
  max-width: 100%;
}

#app h1 {
  display: block;
  min-width: 100%;
  width: 100%;
  text-align: center;
  margin: 0;
  margin-bottom: 1rem;
}
</style>
