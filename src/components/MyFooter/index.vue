<template>
  <div class="todo-footer" v-if="hasTodo">
    <input type="checkbox" :checked="isDoneAll" @change="checkAll" />
    <p class="total-box">已完成：{{ doneTotal }}/全部：{{ allTotal }}</p>
    <button class="delete-all" @click="deleteDoneTodo">清除已完成项目</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  props: ["todoList", "checkAllTodos", "deleteDoneTodos"],
  computed: {
    doneTotal() {
      let i = 0;
      this.todoList.forEach((item) => {
        if (item.done) i++;
      });
      return i;
    },
    allTotal() {
      return this.todoList.length;
    },
    isDoneAll() {
      return this.doneTotal === this.allTotal && this.allTotal > 0;
    },
    hasTodo() {
      return this.allTotal;
    },
  },
  methods: {
    checkAll(e) {
      this.checkAllTodos(e.target.checked);
    },
    deleteDoneTodo(){
      this.deleteDoneTodos();
    }
  },
};
</script>

<style scoped>
.todo-footer {
  width: 700px;
  height: 50px;
  margin: 10px auto 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  display: flex;
  align-items: center;
  padding: 0 10px;
  box-sizing: border-box;
  position: relative;
}

.todo-footer .total-box {
  font-size: 18px;
  margin-left: 2px;
}
.todo-footer .delete-all {
  width: 120px;
  height: 25px;
  background-color: #e35942;
  color: #fff;
  border: none;
  border-radius: 5px;
  position: absolute;
  top: 50%;
  right: 10px;
  transform: translateY(-50%);
}
</style>
