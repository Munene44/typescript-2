<template>
  <div class="container">
    <h1>Todo List</h1>
    <form @submit.prevent="addTask">
      <div class="form-group">
        <label for="task">Task</label>
        <input type="text" class="form-control" id="task" v-model="newTask">
      </div>
      <button type="submit" class="btn btn-primary">Add Task</button>
    </form>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="task.id">
          <th scope="row">{{ index + 1 }}</th>
          <td>{{ task.text }}</td>
          <td>
            <input type="checkbox" v-model="task.completed" @change="markTaskCompleted(task)">
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue'
import { v4 as uuidv4 } from 'uuid'

interface Task {
  id: string
  text: string
  completed: boolean
}

export default defineComponent({
  name: 'TodoList',
  data() {
    return {
      newTask: '',
      tasks: [] as Task[]
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        const task: Task = {
          id: uuidv4(),
          text: this.newTask.trim(),
          completed: false
        }
        this.tasks.push(task)
        this.newTask = ''
      }
    },
    markTaskCompleted(task: Task) {
      task.completed = !task.completed
    }
  }
})
</script>
