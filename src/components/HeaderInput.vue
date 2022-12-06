<template>
  <div>
    <div class="todo-header">
      <input type="text" placeholder="請輸入代辦事項，按回車加入清單" v-model="title" @keyup.enter="add"/>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'HeaderInput',
    props: ['addTodo'],
    data() {
      return {
        title: ''
      }
    },
    methods: {
      GenNonDuplicateID(){
        return Math.random().toString(36).substring(2)
      },
      add() {
        if (!this.title.trim()) return alert('無法設置空代辦事項')
        const todoObj = {id: this.GenNonDuplicateID(), title: this.title, done: false}
        this.addTodo(todoObj)
        this.title = ''
      }
    }
  }
</script>

<style scoped>
  /*header*/
  .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
  }

  .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
  }
</style>
