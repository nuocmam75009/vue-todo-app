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
      v-for="todo in sortedTodos()"
      :key="todo.date"
      :class="{ done: todo.done }"
      >
      <label>
        <input type="checkbox" v-model="todo.done">
        <!-- If checked, done becomes true and vice versa  -->
        {{ todo.title }}
      </label>
    </li>
    </ul>
    <label>
      <input type="checkbox" v-model="hideCompleted"> Hide completed tasks
    </label>
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
}, {
  title: 'Buy groceries',
  done: false,
  date: Date.now()
}, {
  title: 'Design wireframes and UML diagrams for Token.io',
  done: false,
  date: Date.now()
}
]) // Array of tasks

const addTodo = () => {
  // Method to add a new task
  todos.value.push({
    title: newTodo.value,
    done: false,
    date: Date.now()
  })
}

newTodo.value = '' // Reset the input field

const sortedTodos = () => {
  // Method to sort the tasks
 const sortedTodos = todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)
  if (hideCompleted.value) {
    return sortedTodos.filter(todo => !todo.done)
  }
  return sortedTodos
}

const hideCompleted = ref(false) // Hide completed tasks

</script>


<style scoped lang="css">

.done {
  text-decoration: line-through;
  color: grey;
  opacity: .5;
}

</style>
