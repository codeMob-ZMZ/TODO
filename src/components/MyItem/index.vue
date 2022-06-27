<template>
  <div class="todo-item">
    <input type="checkbox" v-model="isDone" />
    <span class="content" v-show="!isEdit">{{ todos.content }}</span>
    <input
      type="text"
      class="edit-inp"
      :value="todos.content"
      v-show="isEdit"
      ref="thisEditInp"
      @blur="editTodo"
      @keyup.enter="editTodo"
    />
    <button class="edit-btn" @click="editTodoIt" v-show="!isEdit">编辑</button>
    <button class="delete-btn" @click="deleteTodo">删除</button>
  </div>
</template>

<script>
export default {
  name: "MyItem",
  data() {
    return {
      isEdit: false,
    };
  },
  props: ["todos"],
  computed: {
    isDone: {
      get() {
        return this.todos.done;
      },
      set() {
        this.$bus.$emit("checkTodos", this.todos.id);
      },
    },
  },
  methods: {
    deleteTodo() {
      if (confirm("确定删除吗？")) {
        this.$bus.$emit("deleteTodos", this.todos.id);
      }
    },
    editTodoIt() {
      this.isEdit = !this.isEdit;
      this.$nextTick(function () {
        this.$refs.thisEditInp.focus();
      });
    },
    editTodo(e) {
      this.isEdit = false;
      if (!e.target.value.trim()) return alert("输入框不能为空！");
      this.$bus.$emit("editTodos", e.target.value, this.todos.id);
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
.edit-inp {
  width: 200px;
  height: 20px;
  border: 1px solid #ccc;
  border-radius: 2px;
  padding: 0 5px;
  box-sizing: border-box;
  outline: none;
  margin-left: 2px;
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
.todo-item .edit-btn {
  width: 50px;
  height: 25px;
  background-color: skyblue;
  color: #fff;
  border: none;
  border-radius: 5px;
  position: absolute;
  top: 50%;
  right: 70px;
  transform: translateY(-50%);
  display: none;
}
.todo-item:hover {
  background-color: rgba(0, 0, 0, 0.3);
}
.todo-item:hover .delete-btn {
  display: block;
}
.todo-item:hover .edit-btn {
  display: block;
}
</style>
