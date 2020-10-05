<template>
  <div>
    <input
      type="text"
      class="todoinp"
      placeholder="Type Somthing..."
      v-model="newTodo"
      @keyup.enter="addTodo"
    />
    <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
      <div class="todo-item-left">
        <input type="checkbox"  v-model="todo.completed">
        <div
          v-if="!todo.edit"
          @dblclick="editTodo(todo)"
          class="todo-item-label" > 
          {{ todo.title }}
        </div>
        <input
          v-else
          type="text"
          class="todo-item-edit"
          v-model="todo.title"
          @blur="doneEdit(todo)"
          @keyup.enter="doneEdit(todo)"
          @keyup.esc="cancelEdit(todo)"

          v-focus
        />
      </div>
      <div class="remove-item" @click="removeTodo(index)">&times;</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ToDoList',
  data () {
    return {
      newTodo: '',
      idForTodo: 3,
      beforeEditCache: '',
      todos: [
        {
          id: 1,
          title: 'test',
          conpleted: false,
          edit: false
        },
        {
          id: 2,
          title: 'SECtest',
          conpleted: false,
          edit: false
        }
      ]
    }
  },
  directives: {
    focus: {
      inserted: function (el) {
        el.focus()
      }
    }
  },
  methods: {
    addTodo () {
      alert('Hello Nigga')
      if (this.newTodo.trim().length === 0) {
        return
      }
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false
      })
      this.newTodo = ''
      this.idForTodo++
    },
    removeTodo (index) {
      this.todos.splice(index, 1)
    },
    editTodo (todo) {
      // alert('test dbbclicked')
      this.beforeEditCache = todo.title
      todo.edit = true
    },
    doneEdit (todo) {
      if (this.newTodo.trim().length === 0) {
        todo.title = this.beforeEditCache
      }
      todo.edit = false
    },
    cancelEdit (todo) {
      todo.title = this.beforeEditCache
      todo.edit = false
    }
  }
}
</script>

<style>
.todoinp {
  height: 20px;
  border-radius: 20px;
  border-style: none;
  width: 50%;
  font-size: 18px;
  background-color: lightgreen;
  padding: 10px 10px;
}
.todo-item {
  cursor: pointer;

  margin-bottom: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.remove-item {
  cursor: pointer;
  margin-left: 14;
}
/* .todo-item-left {
} */
.todo-item-edit {
  height: 20px;
  border-style: none;
  width: 50%;
  font-size: 13px;
  background-color: rgb(164, 209, 164);
  padding: 10px 10px;
}
</style>
