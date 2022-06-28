<template>
  <div class="item">{{ files.content }}</div>
</template>

<script>
export default {
  name: "MyFileItem",
  props: ["files"],
};
</script>

<style scoped>
.item {
  width: 7rem;
  height: 0.6rem;
  border-bottom: 0.01rem solid #ccc;
  display: flex;
  align-items: center;
  padding: 0 0.1rem;
  box-sizing: border-box;
  position: relative;
  font-size: 0.2rem;
  margin: 0.1rem auto 0;
}
</style>
