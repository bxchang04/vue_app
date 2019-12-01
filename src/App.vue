/*
Add a @dblclick attribute in the ToDo label element, which calls a method that sets the ToDo the user just double clicked as the edited ToDo
Add an editing class to the list item that was double clicked: :class="{editing: todo == editedTodo}"
Add some CSS styling to display:block or display:none based on the editing class you added in step 2.
*/


// src/App.vue
<template>
  <div>
    <md-field>
      <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a todo"></md-input>
    </md-field>

    <ul class="todos">
      <li v-for="todo in todos" :key="todo.id">
        {{ todo.label }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: ''
    };
  },
  methods: {
    addTodo() {
      this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false});
      this.currentTodo = '';
    }
  }
};
</script>

<style>
</style>
