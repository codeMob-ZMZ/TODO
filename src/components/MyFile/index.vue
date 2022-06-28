<template>
  <div class="files-box" v-if="hasFiles">
    <h2>已归档任务清单</h2>
    <MyFileItem v-for="files in fileList" :key="files.id" :files="files" />
  </div>
</template>

<script>
import MyFileItem from "../MyFileItem/index";

export default {
  name: "MyFile",
  components: { MyFileItem },
  data() {
    return {
      hasFiles: false,
    };
  },
  props: ["fileList"],
  methods: {
    deleteTodo() {
      if (confirm("确定删除吗？")) {
        this.$bus.$emit("deleteTodos", this.todos.id);
      }
    },
  },
  computed: {
    isHasFiles: {
      get() {
        if (localStorage.getItem("fileTodoList") == null) {
          return false;
        } else {
          return true;
        }
      },
      set(value) {
        this.hasFiles = value;
      },
    },
  },
  created() {
    if (localStorage.getItem("fileTodoList") == null) {
      this.hasFiles = false;
    } else {
      this.hasFiles = true;
    }
  },
  mounted() {
    this.$bus.$on("hasFilesDo", () => {
      this.hasFiles = true;
      console.log(this.hasFiles);
    });
  },
  beforeDestroy() {
    this.$bus.$off("hasFilesDo");
  },
};
</script>

<style scoped>
.files-box {
  width: 100%;
  border: 0.01rem solid #ccc;
  border-radius: 0.05rem;
  margin: 0.5rem auto 0;
  padding-bottom: 0.2rem;
}
.files-box h2 {
  text-align: center;
  font-size: 0.4rem;
}
</style>
