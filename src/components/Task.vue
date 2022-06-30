<template>
  <!-- {{ }} used in html template to write variables -->
  <!-- VS. in React: { } used in JSX && {{}} used only when inline styling -->
  <div
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task.title }}
      <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
      <!-- <=> @click="$emit("delete-task", task.id)" -->
      <!-- VS. in React: -->
      <!-- <=> onClick={() => onDeleteTask(task.id)} -->
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
  // methods: {
  //   onDelete(id) {
  //     //use this.$emit to emit an event; pass the func up to the parent
  //     //this.$emit("name-you-created", param);
  //     this.$emit("delete-task", id);
  //   },
  // },
};
</script>

<style scope>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
