<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label for="title">Task</label>
      <input
        type="text"
        v-model="title"
        name="title"
        id="title"
        placeholder="Add Task"
      />
    </div>
    <div class="form-control">
      <label for="day">Day & Time</label>
      <input
        type="text"
        v-model="day"
        name="day"
        id="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <label for="reminder">Set Reminder</label>
      <input type="checkbox" v-model="reminder" name="reminder" id="reminder" />
      <!-- v-model gives a bind between input and data -->
    </div>

    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>

<script>
export default {
  name: "AddTask",
  // data() <=> states in React
  data() {
    return {
      // initial state || default value for the form
      title: "",
      day: "",
      reminder: false,
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();

      if (!this.title) {
        alert("Please add a task");
        return;
      }

      const newTask = {
        // id: Math.floor(Math.random() * 100),
        // the id will be given by json server
        title: this.title,
        day: this.day,
        reminder: this.reminder,
      };

      //emit upward
      this.$emit("add-task", newTask);

      // clear form
      this.title = "";
      this.day = "";
      this.reminder = false;
    },
  },
};
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>
