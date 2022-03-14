<template>
  <li>
    <label for="">
      <input
        type="checkbox"
        :checked="todo.done"
        @click="handleCheck(todo.id)"
      />
      <span>{{ todo.title }}</span>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
  </li>
</template>

<script>
export default {
  name: 'TdItem',
  props: ['todo', 'checkTodo', 'deleteTodo'],
  methods: {
    handleCheck(id) {
      //   通知app;组件对象将done值取反
      this.checkTodo(id);
    },
    handleDelete(id) {
      if (confirm('请确定是否删除？')) {
        this.deleteTodo(id);
      }
    },
  },
};
</script>

<style scoped>
/* item */
li {
  clear: both;
  display: block;
  padding: 0 10px;
  height: 40px;
  line-height: 40px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  line-height: 40px;
}

li label input {
  margin-right: 10px;
  border-color: #ddd;
}

li .btn {
  display: none;
  float: right;
  margin-top: 6px;
}

li:hover {
  background-color: #f7f7f7;
}

li:hover label {
  color: #424242;
}

li:hover .btn {
  display: block;
}
</style>