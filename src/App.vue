<template>
  <div id="app">
    <div class="wrap">
      <MyHeader :addTodos="addTodos" />
      <MyList
        :todoList="todoList"
        :checkTodos="checkTodos"
        :deleteTodos="deleteTodos"
      />
      <MyFooter
        :todoList="todoList"
        :checkAllTodos="checkAllTodos"
        :deleteDoneTodos="deleteDoneTodos"
      />
    </div>
  </div>
</template>

<script>
import MyHeader from "./components/MyHeader/index.vue";
import MyList from "./components/MyList/index.vue";
import MyFooter from "./components/MyFooter/index.vue";
export default {
  name: "App",
  components: { MyHeader, MyList, MyFooter },
  data() {
    return {
      todoList: JSON.parse(localStorage.getItem("todos")) || [],
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
      console.log(todoId);
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
  },
  watch: {
    todoList: {
      deep: true,
      handler(newValue) {
        localStorage.setItem("todos", JSON.stringify(newValue));
      },
    },
  },
};
</script>

<style>
.wrap {
  width: 750px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  cursor: pointer;
}
</style>
