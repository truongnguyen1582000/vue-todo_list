<template>
  <div class="todo-list">
    <h1>TODOS</h1>
    <TodoForm @formSubmit="addNewTodo" />
    <ul>
      <div class="progress-bar">
        <div
          class="percent-completed"
          :style="{ width: completePercent + '%' }"
        ></div>
      </div>
      <TodoItem
        v-for="todo in filteredTodos"
        :key="todo.id"
        :todo="todo"
        @setStatus="setStatus"
        @removeTodo="removeTodo"
      >
      </TodoItem>
    </ul>
    <TodoSelection
      @changeFilter="handleChangeFilter"
      :counter="
        Math.trunc(todos.length - (todos.length * completePercent) / 100)
      "
      :currentSelection="filter"
      @clearAllCompleted="handleClearAllCompleted"
    />
  </div>
</template>

<script>
import TodoForm from "./TodoForm.vue";
import TodoItem from "./TodoItem.vue";
import TodoSelection from "./TodoSelection.vue";

export default {
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")) || [],
      completePercent: 0,
      filteredTodos: [],
      filter: localStorage.getItem("filter") || "all",
    };
  },

  mounted() {
    this.setFilter(localStorage.getItem("filter") || "all");
  },

  watch: {
    todos: {
      handler: function () {
        this.setFilter(this.filter);

        if (this.todos.length === 0) {
          return;
        }
        this.completePercent =
          (this.todos.filter((todo) => todo.isCompleted === true).length /
            this.todos.length) *
          100;
      },
      deep: true,
    },
    filter: function (newVal) {
      this.setFilter(newVal);
    },
  },
  components: {
    TodoForm,
    TodoItem,
    TodoSelection,
  },
  methods: {
    addNewTodo(val) {
      this.todos.push({
        id: new Date().toISOString(),
        title: val,
        isCompleted: false,
      });

      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    setStatus(id) {
      const todoIdx = this.todos.findIndex((todo) => todo.id === id);
      this.todos[todoIdx].isCompleted = !this.todos[todoIdx].isCompleted;

      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    removeTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },

    handleChangeFilter(val) {
      this.filter = val;
    },

    setFilter(val) {
      if (val === "completed") {
        this.filteredTodos = this.todos.filter(
          (todo) => todo.isCompleted === true
        );
      } else if (val === "active") {
        this.filteredTodos = this.todos.filter(
          (todo) => todo.isCompleted === false
        );
      } else {
        this.filteredTodos = this.todos;
      }
      localStorage.setItem("filter", val);
    },
    handleClearAllCompleted() {
      this.todos = this.todos.filter((todo) => todo.isCompleted === false);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style lang="css" scoped>
h1 {
  text-align: center;
  font-size: 40px;
  font-weight: bold;
  color: #4dba87;
  margin-bottom: 16px;
}

.todo-list {
  width: 400px;
}

ul {
  position: relative;
  box-shadow: 0 3px 4px 1px #d4d4d4;
  border-radius: 4px;
  margin-bottom: 16px;
  overflow: hidden;
  padding-top: 8px;
}

.progress-bar {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  background-color: #caeadb;
  border-radius: 4px;
  height: 9px;
}

.percent-completed {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 0;
  background-color: #4bb986;
  border-radius: inherit;
  transition: all 0.3s ease;
}
</style>