<template>
  <div class="todo-header">
    <h2>猪比小蕾备忘录</h2>
    <input type="text" @keyup.enter="addTodo" />
  </div>
</template>

<script>
import { nanoid } from "nanoid";
export default {
  name: "MyHeader",
  methods: {
    addTodo(e) {
      if (!e.target.value.trim()) return alert("请输入备忘事项！");
      const add = {
        id: nanoid(),
        done: false,
        content: e.target.value,
      };
      this.$emit("addTodos", add);
      e.target.value = "";
    },
  },
};
</script>

<style scoped>
.todo-header {
  width: 7rem;
  margin: 0.1rem auto 0;
  font-size: 0;
}
.todo-header h2 {
  text-align: center;
  font-size: 0.4rem;
}
.todo-header input {
  width: 7rem;
  height: 0.6rem;
  border: 0.01rem solid #ccc;
  border-radius: 0.05rem;
  padding: 0 0.1rem;
  box-sizing: border-box;
}
</style>
