<template>
  <div class="todo-footer" v-show="total">
    <label>
      <input type="checkbox" :checked="isAll" @change="checkAll" />
    </label>
    <span>
      <span>已完成 {{ doneTotal }}</span>
      / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: 'TdFooter',
  props: ['todos', 'checkAllTodo', 'clearAlltodo'],
  computed: {
    total() {
      return this.todos.length;
    },
    doneTotal() {
      return this.todos.reduce((pre, todo) => pre + (todo.done ? 1 : 0), 0);
    },
    isAll() {
      return this.doneTotal === this.total && this.total > 0;
    },
  },
  methods: {
    checkAll(e) {
      this.checkAllTodo(e.target.checked);
    },
    clearAll() {
      if (confirm('是否清除全部已完成任务？')) {
        this.clearAlltodo();
      }
    },
  },
};
</script>

<style scoped>
/* footer */
.todo-footer {
  clear: both;
  padding: 0 10px;
  height: 40px;
  line-height: 40px;
}

.todo-footer label {
  float: left;
}

.todo-footer label input {
  margin-right: 10px;
}

.todo-footer button {
  float: right;
  margin-top: 6px;
}
</style>