<template>
  <div>
    <form @submit.prevent="addTodo">
      <fieldset>
        <input v-model="newTodo" placeholder="Add a new task:">
        <button :disabled="newTodo.length === 0">Add</button>
      </fieldset>
    </form>

    <div v-if="todos.length === 0">No todos 😞</div>
    <div v-else>
      <ul>
        <li
          v-for="todo in sortedTodos()"
          :key="todo.date"
          :class="{ done: todo.done }"
        >
          <label v-if="!isEditing(todo)">
            <input type="checkbox" v-model="todo.done">
            {{ todo.title }}
            <button class="editButton" @click="editTask(todo)">Edit</button>
          </label>
          <div v-else>
            <input v-model="todo.title" @keyup.enter="saveTask(todo)">
            <button @click="saveTask(todo)">Save</button>
          </div>
        </li>
      </ul>
      <!-- <label>
        <input type="checkbox" v-model="hideCompleted"> Hide completed tasks
      </label> -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    // Initialize the component's data
    return {
      newTodo: '',
      todos: [],
      hideCompleted: false,
      editingTask: null
    };
  },
  methods: {
    addTodo() {
      // Add a new todo to the list
      if (this.newTodo.trim()) {
        this.todos.push({ title: this.newTodo, done: false, date: new Date() });
        this.newTodo = '';
      }
    },
    sortedTodos() {
      // Filter the todos
      return this.todos.sort((a, b) => a.date - b.date);
    },
    editTask(todo) {
      // Edit a todo
      this.editingTask = todo;
    },
    saveTask(todo) {
      // Save edited
      this.editingTask = null;
    },
    isEditing(todo) {
      // If todo is being edited
      return this.editingTask === todo;
    }
  }
}
</script>

<style scoped>
.done {
  text-decoration: line-through;
  opacity: .5;
}

.editButton {
  margin-left: 10px;
  font-size: 0.8rem;
  padding: 0.2rem 0.5rem;
}

</style>
