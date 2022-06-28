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
  props: ["todoList"],
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
      this.$emit("checkAllTodos", e.target.checked);
    },
    deleteDoneTodo() {
      this.$emit("deleteDoneTodos");
    },
  },
};
</script>

<style scoped>
.todo-footer {
  width: 7rem;
  height: 0.6rem;
  margin: 0.1rem auto 0.1rem;
  border: 0.01rem solid #ccc;
  border-radius: 0.05rem;
  display: flex;
  align-items: center;
  padding: 0 0.1rem;
  box-sizing: border-box;
  position: relative;
}

.todo-footer .total-box {
  font-size: 0.2rem;
  margin-left: 0.02rem;
}
.todo-footer .delete-all {
  width: 2.2rem;
  height: 0.4rem;
  background-color: #e35942;
  color: #fff;
  border: none;
  border-radius: 0.05rem;
  position: absolute;
  top: 50%;
  right: 0.1rem;
  transform: translateY(-50%);
}
</style>
