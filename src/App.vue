<template>
  <div class='container'>
      <h1>To Do List</h1>
      <md-card class="cardBox">
          <md-field>
            <md-input v-model='currentTodo' @keydown.enter='addTodo(todo)' placeholder='Add a todo'></md-input>
          </md-field>
              <div class='todoBox'>
                <li v-for='(todo, index) in todos' :key='todo.id'>
                  <input class='completeButton' type='checkbox' v-model='todo.completed' >

                      <span class="todo-item-label" :class='{completed: todo.completed}' @dblclick='editTodo(todo)' v-if="!todo.edit">
                          {{todo.label}}
                      </span>

                        <md-input v-else class="todo-item-edit" type="text" v-model='todo.label' @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" @keyup.escape="doneEdit(todo)">
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
      todos: [
        {
          'id': 1,
          'label': 'Make a Vue website app',
          'completed': true,
          'edit': false
        },
      ],
      currentTodo: '',
      editedTodo: null
    }
  },
  methods: {
      addTodo() {

        if (this.currentTodo.trim() == 0) {
          return
        }
        this.todos.push({
          id:this.todos.length,
          label: this.currentTodo,
          completed: false,
          edit: false
        });
        this.currentTodo = '';
      },
      removeTodo(index) {
        this.todos.splice(index,1)
      },
      editTodo(todo) {
        todo.edit = true
      },
      doneEdit(todo) {
        todo.edit = false
      }
  }
}
</script>

<style>

#app {
  font-family: 'Roboto', Helvetica, Arial, sans-serif;
}

li {
  list-style: none;
}
.container {
  width: 50%;
  margin: auto;
  text-align: center;
}

.completed {
  text-decoration: line-through;
}
.todoBox {
  font-size: 1.5em;
}
.cardBox {
padding: 10px;
}

.closeButton {
  float: right;
}

.completeButton {
  float: left;
}

</style>
