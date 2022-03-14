<template>
  <ul class="todo-main">
    <TdItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      :checkTodo="checkTodo"
      :deleteTodo="deleteTodo"
    />
  </ul>
</template>

<script>
import TdItem from './TdItem.vue';
export default {
  name: 'TdList',
  components: { TdItem },
  props: ['todos', 'checkTodo', 'deleteTodo'],
};
</script>

<style scoped>
/* main */
.todo-main {
  margin-bottom: 10px;
  border: 1px solid #ddd;
  border-bottom: none;
  border-radius: 4px;
}

.todo-empty {
  padding: 10px;
  line-height: 40px;
  text-align: center;
  color: #9e9e9e;
  border-bottom: 1px solid #ddd;
}
</style>