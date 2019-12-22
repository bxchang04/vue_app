<template>
  <div class="container">
    <h1> Your Todo List </h1>
    <md-card class="todoBox">
      <md-field>
        <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add an item to your todo list"></md-input>
      </md-field>

      <div class="todos">
        <li v-for="todo in todos" :key="todo.id">

          <input class ='completeButton' type='checkbox' v-model="todo.completed">
            <span
            class="todo-item-label"
            :class='{completed: todo.completed}'
            @dblclick='editTodo(todo)'
            v-if="!todo.edit">
              {{todo.label}}
            </span>
            <md-input v-else class="todo-item-edit"
            type="text" v-model='todo.label'
            @keyup.enter="completedEdit(todo)">
          </md-input>

          <md-raised class='closeButton' @click="removeTodo(index)">X</md-raised>
        </li>
      </div>

    </md-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: '',
      editedTodo: null
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        edit: false
        });
      this.currentTodo = ''
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
     todo.edit = true;
    },
    completedEdit(todo) {
      todo.edit = false;
    }
  }
};
</script>

<style>
li {
  list-style: none;
}
.container {
  margin: auto;
  text-align: center;
  width: 50%;
}
.completed {
  text-decoration: line-through;
}
.todoBox {
  font-size: 1.5em;
  padding: 0px 5px 2px 5px;
}
.cardBox {
padding: 5px;
}
.closeButton {
  float: left;
}
.closeButton:hover {
  cursor: pointer;
  transition: 0.2s ease;
    color: red
}
.completeButton {
  float: right;
}
.todos {
  margin: 10px;
}
</style>
