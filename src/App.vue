<!-- output -->
<template>
  <div class="container">
    <Header
      @toggle-add-task="toggleAddTask"
      title="Task Tracker"
      :showAddTask="showAddTask"
    />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
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
import AddTask from "./components/AddTask";

export default {
  name: "App",
  // register components here after importing them:
  components: { Header, Tasks, AddTask },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },
  methods: {
    async deleteTask(id) {
      if (confirm("Are you sure you want to delete this task?")) {
        const res = fetch(`http://localhost:5000/tasks/${id}`, {
          method: "DELETE",
        });
        // res.status === 200
        //   ? (this.tasks = this.tasks.filter((task) => task.id !== id))
        //   : alert("Something went wrong");
        console.log(res);
        console.log(res.status);
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    async onToggleReminder(id) {
      //fetch the task wanted to be toggled
      const taskToToggle = await this.fetchTask(id);
      const updatedTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

      //make the request
      const res = await fetch(`http://localhost:5000/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(updatedTask), //PUT the upd task back to api
      });
      const data = await res.json();

      //frontend update
      this.tasks = this.tasks.map((task) =>
        // task.id === id ? { ...task, reminder: !task.reminder } : task
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },

    // addTask(task) {
    //   // this.tasks.push(task);
    //   this.tasks = [...this.tasks, task];
    // },
    async addTask(task) {
      const res = await fetch("http://localhost:5000/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });

      const data = await res.json();

      this.tasks = [...this.tasks, data];
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    async fetchTasks() {
      const res = await fetch("http://localhost:5000/tasks");

      const data = await res.json();

      return data;
    },
    // fetch a single task for update
    async fetchTask(id) {
      const res = await fetch(`http://localhost:5000/tasks/${id}`);

      const data = await res.json();

      return data;
    },
  },
  // life cycle
  async created() {
    this.tasks = await this.fetchTasks();
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
