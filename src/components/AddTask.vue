<template>
     <form @submit="onSubmit" class="add-form">
      <div class="form-control">
        <label for="text">Task</label>
        <input type="text" name="text" v-model="text" placeholder="Add Task" />
      </div>
      <div class="form-control">
        <label for="day">Day & Time</label>
        <input type="text" name="day" v-model="day" placeholder="Add Day & Time" />
      </div>
      <div class="form-control form-control-check">
        <label for="reminder">Set Reminder</label>
        <input type="checkbox" v-model="reminder" name="reminder" />
      </div>

      <input type="submit" value="Save Task" class="btn btn-block">
    </form>
</template>

<script>
export default {
    name: 'AddTask',
    data() {
      return {
        text: '',
        day: '',
        reminder: false
      }
    },
    methods: {
      onSubmit(e) {
        e.preventDefault()

        if (!this.text) {
          alert('Please describe the task')
          return
        }

        if (!this.day) {
          alert('Please specify the date time')
          return
        }

        const newTask = {
          id: Math.floor(Math.random() * 100000),
          text: this.text,
          day: this.day,
          reminder: this.reminder
        }

        this.$emit('add-task', newTask)

        this.text = ''
        this.day = ''
        this.reminder = false
      }
    },
    emits: ['add-task']
}
</script>
