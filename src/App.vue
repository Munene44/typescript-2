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
