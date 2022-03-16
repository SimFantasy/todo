<template>
  <ul class="todo-main">
    <transition-group name="todo" appear>
      <TdItem v-for="todo in todos" :key="todo.id" :todo="todo" />
    </transition-group>
  </ul>
</template>

<script>
import TdItem from './TdItem.vue';
export default {
  name: 'TdList',
  components: { TdItem },
  props: ['todos'],
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

.todo-enter-active {
  animation: simT 0.3s linear;
}

.todo-leave-active {
  animation: simT 0.3s linear reverse;
}

@keyframes simT {
  from {
    transform: translateX(100%);
    opacity: 1;
  }
  to {
    transform: translateX(0);
    opacity: 0;
  }
}
</style>