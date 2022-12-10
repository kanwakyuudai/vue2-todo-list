<template>
  <li>
    <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)"/>
    <span v-show='!showEdit' @dblclick="toggleEdit(todo)">{{todo.title}}</span>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">刪除事項</button>
    <input v-show='showEdit'
    class="edit"
    type="text"
    v-model="todo.title"
    @blur="handleEdited(todo)"
    @keyup.enter="handleEdited(todo)"
    @keyup.esc="handleCancelEdit(todo)"/>
  </li>
</template>

<script>
  export default {
    name: 'ListItem',
    props: ['todo','checkTodo','deleteTodo', 'editTodo', 'doneEdit', 'cancelEdit', 'editedTodo'],
    data() {
      return {
        showEdit: false
      }
    },
    methods: {
      handleCheck(id) {
        this.checkTodo(id)
      },
      handleDelete(id) {
        this.deleteTodo(id)
      },
      toggleEdit(todo) {
        this.showEdit = true
        this.editTodo(todo)
      },
      handleEdited(todo) {
        this.doneEdit(todo)
        this.showEdit = false
      },
      handleCancelEdit(todo) {
        this.cancelEdit(todo)
        this.showEdit = false
      }
    }
  }
</script>

<style scoped>
  /*item*/
  li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
  }

  li label {
    float: left;
    cursor: pointer;
  }

  li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }

  li button {
    float: right;
    display: none;
    margin-top: 3px;
  }

  li:before {
    content: initial;
  }

  li:last-child {
    border-bottom: none;
  }

  li:hover{
    background-color: #ddd;
  }

  li:hover button{
    display: block;
  }
</style>
