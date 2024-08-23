<template>
  <form actions="" @submit.prevent="addTodo">
    <fieldset role="group">
      <input
        v-model="todo"
        type="text"
        placeholder="Tasks to do:">
      <button>Add</button>
  </fieldset>
  </form>

  <div v-if="todos.length === 0">No task to do</div>
</template>



<script setup>

import { ref } from 'vue'

const todo = ref('') // Task to do
const todos = ref([]) // Array of tasks
const addTodo = () => {
  // Method to add a new task
  todos.value.push({
    title: todo.value,
    done: false,
    date: Date.now()
  })
}

</script>


<style scoped lang="scss">

</style>
