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
    <button class="file-btn" @click="fileTodoIt">归档</button>
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
    fileTodoIt() {
      this.$bus.$emit("fileTodos", this.todos.id);
      this.$bus.$emit("hasFilesDo");
    },
  },
};
</script>

<style scoped>
.todo-item {
  width: 7rem;
  height: 0.6rem;
  border-bottom: 0.01rem solid #ccc;
  display: flex;
  align-items: center;
  padding: 0 0.1rem;
  box-sizing: border-box;
  position: relative;
}
.edit-inp {
  width: 2rem;
  height: 0.4rem;
  border: 0.01rem solid #ccc;
  border-radius: 0.02rem;
  padding: 0 0.05rem;
  box-sizing: border-box;
  outline: none;
  margin-left: 0.02rem;
}
.todo-item:last-of-type {
  border-bottom: none;
}
.todo-item .content {
  font-size: 0.2rem;
  margin-left: 0.02rem;
}
.todo-item .delete-btn {
  width: 1rem;
  height: 0.4rem;
  background-color: #e35942;
  color: #fff;
  border: none;
  border-radius: 0.05rem;
  position: absolute;
  top: 50%;
  right: 0.1rem;
  transform: translateY(-50%);
  display: none;
}
.todo-item .edit-btn {
  width: 1rem;
  height: 0.4rem;
  background-color: skyblue;
  color: #fff;
  border: none;
  border-radius: 0.05rem;
  position: absolute;
  top: 50%;
  right: 1.2rem;
  transform: translateY(-50%);
  display: none;
}
.todo-item .file-btn {
  width: 1rem;
  height: 0.4rem;
  background-color: pink;
  color: #fff;
  border: none;
  border-radius: 0.05rem;
  position: absolute;
  top: 50%;
  right: 2.3rem;
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
.todo-item:hover .file-btn {
  display: block;
}
</style>
