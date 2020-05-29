<template>
  <div id="app">
    <input type="text" v-model="state.input" />
    <button @click="addTodo">
      Add TODO
    </button>

    <p v-for="(todo, index) in state.todos" :key="index">
      {{todo}}
      <button @click="completeTodo(index)">
        Complete
      </button>
    </p>

    <p>Completed</p>
    <p v-for="(todo, index) in state.completedTodos" :key="index">
      {{todo}}
    </p>
  </div>
</template>

<script>
import { defineComponent, reactive } from 'vue'

export default defineComponent({
  setup() {
    const state = reactive({
      input: "",
      todos: [],
      completedTodos: [],
    })

    function addTodo() {
      state.todos = [...state.todos, state.input]
      state.input = ""
    }

    function completeTodo(index) {
      state.completedTodos = [...state.completedTodos, state.todos[index]]

      state.todos.splice(index, 1)
      state.todos = [...state.todos]
    }

    return {
      state,
      addTodo,
      completeTodo
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
