<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <HeaderInput :addTodo="addTodo"></HeaderInput>
        <BodyList :todoSet="todoSet" :checkTodo="checkTodo" :deleteTodo="deleteTodo"></BodyList>
        <FooterArea :todoSet="todoSet" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"></FooterArea>
      </div>
    </div>
  </div>
</template>

<script>
import HeaderInput from './components/HeaderInput.vue';
import BodyList from './components/BodyList.vue';
import FooterArea from './components/FooterArea.vue'

export default {
  name: 'App',
  components: {HeaderInput, BodyList, FooterArea},
  data() {
    return {
      todoSet: JSON.parse(localStorage.getItem('todo-list-data')) || []
    }
  },
  methods: {
    addTodo(item) {
      this.todoSet.unshift(item)
    },
    checkTodo(id) {
      this.todoSet.forEach(item => {
        if(item.id === id) item.done = !item.done
      })
    },
    deleteTodo(id) {
      this.todoSet = this.todoSet.filter(item => item.id !== id)
    },
    checkAllTodo(done) {
      this.todoSet.forEach(item => {
        item.done = done
      })
    },
    clearAllTodo() {
      this.todoSet = this.todoSet.filter(item => !item.done)
    }
  },
  watch: {
    todoSet: {
      deep: true,
      handler(newTodoSet) {
        localStorage.setItem('todo-list-data', JSON.stringify(newTodoSet))
      }
    }
  }
}
</script>

<style>
  /*base*/
  body {
    zoom: 1.5;
    background: #fff;
  }
  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }
  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }
  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }
  .btn:focus {
    outline: none;
  }
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
