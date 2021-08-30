<template>
  <li>
    <div @click="setStatus(todo.id)" class="check-btn">
      <i class="far fa-check-square" v-if="!todo.isCompleted"></i>
      <i class="fas fa-check-square" v-else></i>
    </div>
    <p :class="{ completed: todo.isCompleted }" @click="setStatus(todo.id)">
      {{ todo.title }}
    </p>
    <button @click="removeTodo(todo.id)">
      <i class="fas fa-trash-alt"></i>
    </button>
  </li>
</template>

<script>
export default {
  inject: ["setStatus", "removeTodo"],
  props: ["todo"],
};
</script>

<style lang="css" scoped>
.check-btn {
  margin-right: 16px;
  margin-left: 8px;
}

li {
  display: flex;
  align-items: center;
  padding: 8px;
}

li:not(:first-of-type) {
  border-top: 1px solid #000;
}

p {
  cursor: pointer;
  word-break: break-all;
}

button {
  margin-left: auto;
  background-color: transparent;
  border: none;
  cursor: pointer;
  font-size: 24px;
}

.completed {
  text-decoration: line-through;
  opacity: 0.5;
}
</style>