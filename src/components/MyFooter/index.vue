<template>
  <div class="todo-footer">
    <input type="checkbox" />
    <p class="total-box">已完成：0/全部：3</p>
    <button class="delete-all">清除已完成项目</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
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
