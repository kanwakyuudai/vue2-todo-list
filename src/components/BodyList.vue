<template>
  <ul class="todo-main">
    <ListItem
    v-for="todoObj in todoSet"
    :key="todoObj.id"
    :todo="todoObj"
    :checkTodo="checkTodo"
    :deleteTodo="deleteTodo"
    ></ListItem>
  </ul>
</template>

<script>
  import ListItem from './ListItem.vue';

  export default {
    name: 'BodyList',
    components: {ListItem},
    props: ['todoSet', 'checkTodo', 'deleteTodo']
  }
</script>

<style scoped>
  /*main*/
  .todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
  }

  .todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
  }
</style>
