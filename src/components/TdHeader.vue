<template>
  <div class="todo-header">
    <input
      type="text"
      v-model="title"
      placeholder="请输入您的任务名称，按回车键确认"
      @keyup.enter="add"
    />
  </div>
</template>

<script>
import { nanoid } from 'nanoid';
export default {
  name: 'TdHeader',
  data() {
    return {
      title: '',
    };
  },
  methods: {
    add() {
      // 校验输入数据
      if (!this.title.trim()) {
        return alert('任务不能为空');
      }
      // 将用户的输入包装成一个对象
      const todoObj = {
        id: nanoid(),
        title: this.title,
        done: false,
      };
      //   通知app组件输入一个TODO对象;
      this.$emit('addTodo', todoObj);
      this.title = '';
    },
  },
};
</script>

<style scoped>
/* Header */
.todo-header {
  margin-bottom: 10px;
}

.todo-header input {
  padding: 0 8px;
  width: 600px;
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 4px;
  text-align: left;
  color: #757575;
}

.todo-header input:focus {
  border-color: rgba(82, 168, 236, 0.8);
  color: #424242;
}
</style>