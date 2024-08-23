<template>
  <form actions="" @submit.prevent="addTodo">
    <fieldset role="group">
      <input
        v-model="newTodo"
        type="text"
        placeholder="Tasks to do:">
      <button :disabled="newTodo.length === 0">Add</button>
  </fieldset>
  </form>

  <div v-if="todos.length === 0">No task to do</div>
  <div v-else>
    <ul>
      <li
      v-for="todo in todos"
      :key="todo.date"
      >
      <label>
        <input type="checkbox" v-model="todo.completed">
        <!-- If checked, done becomes true and vice versa  -->
        {{ todo.title }}
      </label>
    </li>

    </ul>
  </div>
</template>



<script setup>

import { ref } from 'vue'

const newTodo = ref('') // Task to do
const todos = ref([{
  title: 'Finish Fanprime technical test',
  done: true,
  date: Date.now()
}, {
  title: 'Go to the gym',
  done: false,
  date: Date.now()
}]) // Array of tasks

const addTodo = () => {
  // Method to add a new task
  todos.value.push({
    title: newTodo.value,
    done: false,
    date: Date.now()
  })
}

newTodo.value = '' // Reset the input field

</script>


<style scoped lang="scss">

</style>
