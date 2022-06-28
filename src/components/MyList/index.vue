<template>
  <div class="todo-list">
    <transition-group
      appear
      enter-active-class="animate__animated animate__bounceInRight"
      leave-active-class="animate__animated animate__backOutLeft"
    >
      <MyItem v-for="todos in todoList" :key="todos.id" :todos="todos" />
    </transition-group>
  </div>
</template>

<script>
import MyItem from "../MyItem/index.vue";
export default {
  name: "TodoList",
  components: {
    MyItem,
  },
  props: ["todoList"],
};
</script>

<style scoped>
.todo-list {
  width: 7rem;
  margin: 0.1rem auto 0;
  border: 0.01rem solid #ccc;
  border-radius: 0.05rem;
}
</style>
