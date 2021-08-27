<template>
  <div id="app">
    <TodoList />
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  components: {
    TodoList,
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  user-select: none;
}

body {
  display: flex;
  margin-top: 100px;
  justify-content: center;
  font-family: "Comfortaa", cursive;
  font-size: 24px;
  background-color: #f5f5f5;
}
</style>
