<template>
  <div :key="task.id" v-for="task in tasks">
    <Task :task="task" />
    <!-- VS. in React:  -->
    <!-- <Task task={task} /> -->
  </div>
</template>

<script>
import Task from "./Task.vue";

export default {
  name: "Tasks",
  props: {
    tasks: {
      type: Array,
    },
  },
  components: { Task },
};
</script>
