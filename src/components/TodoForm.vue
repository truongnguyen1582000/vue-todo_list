<template>
  <form @submit.prevent="addNewTodo(value)">
    <input type="text" v-model="value" placeholder="What need to be done?" />
  </form>
</template>

<script>
export default {
  data() {
    return {
      value: "",
    };
  },
  inject: ["addNewTodo"],
};
</script>

<style lang="css" scoped>
form {
  margin-bottom: 16px;
}
input {
  width: 100%;
  outline: none;
  padding: 16px;
  padding-left: 24px;
  margin-bottom: 8px;
  border: none;
  border-radius: 12px;
  box-shadow: 0 3px 4px 1px #d4d4d4;

  font-size: 16px;
}
</style>