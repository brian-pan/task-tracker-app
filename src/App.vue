<!-- output -->
<template>
  <div class="container">
    <Header title="Task Tracker" />
    <Tasks
      :tasks="tasks"
      @delete-task="deleteTask"
      @toggle-reminder="onToggleReminder"
    />
    <!-- use v-bind when you want the value to be 'dynamic'; variable change values; not fixed -->
  </div>
</template>

<!-- logic -->
<script>
import Header from "./components/Header";
import Tasks from "./components/Tasks";

export default {
  name: "App",
  // register components here after importing them:
  components: { Header, Tasks },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    deleteTask(id) {
      if (confirm("Are you sure you want to delete this task?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    onToggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
  },
  // life cycle
  created() {
    this.tasks = [
      {
        id: 1,
        title: "Learn Vue",
        day: "Monday Jun 12",
        reminder: true,
      },
      {
        id: 2,
        title: "Learn Vuex",
        day: "Monday Jun 19",
        reminder: true,
      },
      {
        id: 3,
        title: "Learn Vue Router",
        day: "Tuesday Jul 5",
        reminder: false,
      },
    ];
  },
};
</script>

<!-- style -->
<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
