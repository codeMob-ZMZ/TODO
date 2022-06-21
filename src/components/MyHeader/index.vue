<template>
  <div class="todo-header">
    <input type="text" @keyup.enter="addTodo" />
  </div>
</template>

<script>
import { nanoid } from "nanoid";
export default {
  name: "MyHeader",
  props: ["addTodos"],
  methods: {
    addTodo(e) {
      if (!e.target.value.trim()) return alert("请输入备忘事项！");
      const add = {
        id: nanoid(),
        done: false,
        content: e.target.value,
      };
      this.addTodos(add);
      e.target.value = "";
    },
  },
};
</script>

<style scoped>
.todo-header {
  width: 700px;
  margin: 10px auto 0;
}
.todo-header input {
  width: 700px;
  height: 30px;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 0 10px;
  box-sizing: border-box;
}
</style>
