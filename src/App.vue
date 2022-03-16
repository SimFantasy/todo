<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <TdHeader @addTodo="addTodo" />
        <TdList :todos="todos" />
        <TdFooter
          :todos="todos"
          @checkAllTodo="checkAllTodo"
          @clearAlltodo="clearAlltodo"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TdHeader from './components/TdHeader.vue';
import TdList from './components/TdList.vue';
import TdFooter from './components/TdFooter.vue';

export default {
  name: 'App',
  components: { TdHeader, TdList, TdFooter },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem('todos')) || [],
    };
  },
  methods: {
    //   添加todo
    addTodo(todoObj) {
      this.todos.unshift(todoObj);
    },
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.done = !todo.done;
      });
    },
    updataTodo(id, title) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.title = title;
      });
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    checkAllTodo(done) {
      this.todos.forEach((todo) => {
        todo.done = done;
      });
    },
    clearAlltodo() {
      this.todos = this.todos.filter((todo) => !todo.done);
    },
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem('todos', JSON.stringify(value));
      },
    },
  },
  mounted() {
    this.$bus.$on('checkTodo', this.checkTodo);
    this.$bus.$on('deleteTodo', this.deleteTodo);
    this.$bus.$on('updataTodo', this.updataTodo);
  },
  beforeDestroy() {
    this.$bus.$off('checkTodo');
    this.$bus.$off('deleteTodo');
    this.$bus.$off('updataTodo');
  },
};
</script>

<style>
/* base */
* {
  margin: 0;
  padding: 0;
  outline: none;
  font-size: 14px;
  color: #757575;
}

ul,
li {
  list-style: none;
}

.btn {
  display: inline-block;
  padding: 4px 8px;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  border-radius: 2px;
  cursor: pointer;
  border: 0;
}

.btn-danger {
  background-color: #da4f49;
  color: #fff;
}

.btn-danger:hover {
  background-color: #bd362f;
}

.btn-info {
  margin-right: 10px;
  background-color: #3c96ff;
  color: #fff;
}

.btn-info:hover {
  background-color: #50a1ff;
}

.todo-container {
  margin: 40px auto;
  width: 640px;
  overflow: hidden;
}

.todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
}
</style>