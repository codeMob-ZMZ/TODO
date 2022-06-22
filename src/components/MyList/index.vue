<template>
  <div class="todo-list">
    <MyItem v-for="todos in todoList" :key="todos.id" :todos="todos" />
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
