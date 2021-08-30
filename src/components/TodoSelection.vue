<template>
  <div class="selection">
    <div class="selection-top">
      <button
        @click="changeFilter('all')"
        :class="{ selected: this.currentSelection === 'all' }"
      >
        All
      </button>
      <button
        @click="changeFilter('active')"
        :class="{ selected: this.currentSelection === 'active' }"
      >
        Active
      </button>
      <button
        @click="changeFilter('completed')"
        :class="{ selected: this.currentSelection === 'completed' }"
      >
        Completed
      </button>
      <p class="counter">{{ counter }} left</p>
    </div>
    <button @click="clearAllCompleted" class="clear-btn">CLEAR COMPLETE</button>
  </div>
</template>

<script>
export default {
  props: ["counter", "currentSelection"],
  inject: ["changeFilter", "clearAllCompleted"],
};
</script>

<style lang="css" scoped>
button {
  font-weight: bold;
  border: none;
  padding: 8px;
  cursor: pointer;
  margin: 1px;
  outline: none;
  border-radius: 6px;
}

.clear-btn {
  color: white;
  background-color: #4cba86;
  border-radius: 4px;
  margin-top: 8px;
  width: 100%;
}

.clear-btn:active {
  transform: scale(0.96);
  transition: scale 0.3s ease;
}

.selection {
  padding-top: 8px;
}
.selection-top {
  display: flex;
}

.selection-top p {
  margin-left: auto;
}

.selected {
  background-color: #eaf7f1;
  color: #4cba86;
  box-shadow: 0 0 1px 1px rgb(0, 148, 20);
}
</style>