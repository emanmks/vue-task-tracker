<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask" />

    <div v-if="showAddTask">
      <AddTask @add-task="addTask" />
    </div>

    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>

<script>

import Header from './components/Header.vue'
import AddTask from './components/AddTask.vue'
import Tasks from './components/Tasks.vue'

export default {
  name: 'App',
  components: {
    Header,
    AddTask,
    Tasks,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  created() {
    this.tasks = [
      {
        "id": "1",
        "text": "Doctors Appointment",
        "day": "March 5th at 2:30pm",
        "reminder": true
      },
      {
        "id": "2",
        "text": "Meeting with boss",
        "day": "March 6th at 1:30pm",
        "reminder": true
      },
      {
        "id": "3",
        "text": "Food shopping",
        "day": "March 7th at 2:00pm",
        "reminder": false
      }
    ]
  },
  methods: {
    deleteTask(id) {
      if (confirm("Are you sure?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder} : task)
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
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

/* Form */
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
