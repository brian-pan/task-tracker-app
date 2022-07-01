<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      :text="showAddTask ? 'Close' : 'Add Task'"
      :color="showAddTask ? 'red' : 'green'"
      @btn-click="$emit('toggle-add-task')"
    />
  </header>
</template>

<script>
import Button from "./Button.vue";

export default {
  name: "Header",
  props: {
    title: {
      type: String,
      default: "Hello World",
    },
    showAddTask: {
      type: Boolean,
      default: false,
    },
  },
  components: { Button },
};
</script>

<style scoped>
/* scoped means style only apply to this component */
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
