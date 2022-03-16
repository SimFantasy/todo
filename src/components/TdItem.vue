<template>
  <li>
    <label for="">
      <input
        type="checkbox"
        :checked="todo.done"
        @click="handleCheck(todo.id)"
      />
      <span v-show="!todo.isEdit">{{ todo.title }}</span>
      <input
        type="text"
        class="edit-input"
        :value="todo.title"
        v-show="todo.isEdit"
        @blur="handleBlur(todo, $event)"
        ref="inputTitle"
      />
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
    <button
      class="btn btn-info"
      @click="handleEdit(todo)"
      v-show="!todo.isEdit"
    >
      编辑
    </button>
  </li>
</template>

<script>
export default {
  name: 'TdItem',
  props: ['todo'],
  methods: {
    handleCheck(id) {
      //   通知app;组件对象将done值取反
      //   this.checkTodo(id);
      this.$bus.$emit('checkTodo', id);
    },
    handleDelete(id) {
      if (confirm('请确定是否删除？')) {
        // this.deleteTodo(id);
        this.$bus.$emit('deleteTodo', id);
      }
    },
    handleEdit(todo) {
      if (Object.prototype.hasOwnProperty.call(todo, 'isEdit')) {
        todo.isEdit = true;
      } else {
        this.$set(todo, 'isEdit', true);
      }
      this.$nextTick(function () {
        this.$refs.inputTitle.focus();
      });
    },
    handleBlur(todo, e) {
      todo.isEdit = false;
      if (!e.target.value.trim()) return alert('输入不能为空');
      this.$bus.$emit('updataTodo', todo.id, e.target.value);
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

.edit-input {
  padding: 2px 8px;
  border: 1px solid #ddd;
  border-radius: 2px;
  color: #757575;
}
</style>