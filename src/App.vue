<template>
  <div>
    <TodoList />
  </div>
</template>
<script>
import TodoList from "./components/TodoList.vue";
export default {
  name: "Darsvue1App",
  components: {
    TodoList,
  },

  data() {
    return {};
  },

  mounted() {},

  methods: {},
};
</script>

<style lang="scss" >
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-size: 18px;
  font-family: "sans-serif";
}
</style>