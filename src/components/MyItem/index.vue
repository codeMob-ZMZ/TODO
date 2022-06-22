<template>
  <div class="todo-item">
    <input type="checkbox" v-model="isDone" />
    <span class="content">{{ todos.content }}</span>
    <button class="delete-btn" @click="deleteTodo">删除</button>
  </div>
</template>

<script>
export default {
  name: "MyItem",
  props: ["todos", "checkTodos", "deleteTodos"],
  computed: {
    isDone: {
      get() {
        return this.todos.done;
      },
      set() {
        this.checkTodos(this.todos.id);
      },
    },
  },
  methods: {
    deleteTodo() {
      this.deleteTodos(this.todos.id);
    },
  },
};
</script>

<style scoped>
.todo-item {
  width: 700px;
  height: 40px;
  border-bottom: 1px solid #ccc;
  display: flex;
  align-items: center;
  padding: 0 10px;
  box-sizing: border-box;
  position: relative;
}
.todo-item:last-of-type {
  border-bottom: none;
}
.todo-item .content {
  font-size: 18px;
  margin-left: 2px;
}
.todo-item .delete-btn {
  width: 50px;
  height: 25px;
  background-color: #e35942;
  color: #fff;
  border: none;
  border-radius: 5px;
  position: absolute;
  top: 50%;
  right: 10px;
  transform: translateY(-50%);
  display: none;
}
.todo-item:hover {
  background-color: rgba(0, 0, 0, 0.3);
}
.todo-item:hover .delete-btn {
  display: block;
}
</style>
