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
  width: 700px;
  margin: 10px auto 0;
  border: 1px solid #ccc;
  border-radius: 5px;
}
</style>
