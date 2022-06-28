<template>
  <div id="app">
    <div class="wrap">
      <MyHeader @addTodos="addTodos" />
      <MyList :todoList="todoList" />
      <MyFooter
        :todoList="todoList"
        @checkAllTodos="checkAllTodos"
        @deleteDoneTodos="deleteDoneTodos"
      />
      <MyFile :fileList="fileList" />
    </div>
  </div>
</template>

<script>
import MyHeader from "./components/MyHeader/index.vue";
import MyList from "./components/MyList/index.vue";
import MyFooter from "./components/MyFooter/index.vue";
import MyFile from "./components/MyFile/index.vue";
export default {
  name: "App",
  components: { MyHeader, MyList, MyFooter, MyFile },
  data() {
    return {
      todoList: JSON.parse(localStorage.getItem("todos")) || [],
      fileList: JSON.parse(localStorage.getItem("fileTodoList")) || [],
    };
  },
  methods: {
    // 增加一个备忘事项
    addTodos(todoObj) {
      this.todoList.unshift(todoObj);
    },
    // 勾选对应事项
    checkTodos(todoId) {
      this.todoList.forEach((item) => {
        if (item.id === todoId) item.done = !item.done;
      });
    },
    // 删除对应事项
    deleteTodos(todoId) {
      this.todoList = this.todoList.filter((item) => {
        return item.id != todoId;
      });
    },
    // 全选事项
    checkAllTodos(isAll) {
      this.todoList.forEach((item) => {
        item.done = isAll;
      });
    },
    // 清除已完成事项
    deleteDoneTodos() {
      this.todoList = this.todoList.filter((item) => {
        return !item.done;
      });
    },
    // 编辑
    editTodos(value, index) {
      this.todoList.forEach((item) => {
        if (item.id == index) item.content = value;
      });
    },
    // 归档
    fileTodos(index) {
      this.todoList.forEach((item) => {
        if (item.id == index) {
          this.fileList.unshift(item);
        }
      });
      this.todoList = this.todoList.filter((item) => {
        return item.id != index;
      });
    },
  },
  watch: {
    todoList: {
      deep: true,
      handler(newValue) {
        localStorage.setItem("todos", JSON.stringify(newValue));
      },
    },
    fileList: {
      deep: true,
      handler(newValue) {
        localStorage.setItem("fileTodoList", JSON.stringify(newValue));
        console.log(newValue)
      },
    },
  },
  mounted() {
    this.$bus.$on("checkTodos", this.checkTodos);
    this.$bus.$on("deleteTodos", this.deleteTodos);
    this.$bus.$on("editTodos", this.editTodos);
    this.$bus.$on("fileTodos", this.fileTodos);
  },
  beforeDestroy() {
    this.$bus.$off("checkTodos");
    this.$bus.$off("deleteTodos");
    this.$bus.$off("editTodos");
    this.$bus.$off("fileTodos");
  },
};
</script>

<style>
.wrap {
  width: 100%;
  border: 0.01rem solid #ccc;
  border-radius: 0.05rem;
  margin: 0.5rem auto 0;
}

button {
  cursor: pointer;
}
</style>
