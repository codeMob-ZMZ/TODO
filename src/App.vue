<template>
  <div id="app">
    <div class="wrap">
      <MyHeader :addTodos="addTodos" />
      <MyList :todoList="todoList" :checkTodos="checkTodos" />
      <MyFooter />
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
      todoList: [
        {
          id: "001",
          done: false,
          content: "学习",
        },
        {
          id: "002",
          done: false,
          content: "吃饭",
        },
        {
          id: "003",
          done: true,
          content: "玩耍",
        },
      ],
    };
  },
  methods: {
    // 增加一个备忘事项
    addTodos(todoObj) {
      this.todoList.unshift(todoObj);
    },
    // 勾选对应事项
    checkTodos(id) {
      console.log(id);
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
