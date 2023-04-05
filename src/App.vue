<template>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0/dist/css/bootstrap.min.css">
  <div class="container mt-3">
    <form @submit.prevent="add">
      <div class="input-group">
        <input type="text" class="form-control" placeholder="Add a new todo item" v-model="todo">
        <button type="submit" class="btn btn-primary">Add</button>
      </div>
    </form>
    <div class="list-group mt-3">
      <div v-for="(todo, index) of todos" :key="todo.id" class="list-group-item">
        <div class="form-check">
          <input type="checkbox" class="form-check-input" v-model="todo.completed">
          <label class="form-check-label" :class="{ 'text-muted': todo.completed }">{{ todo.todo }}</label>
        </div>
        <button type="button" class="btn btn-danger btn-sm" @click="deleteTodo(index)">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
export default {
  name: "App",
  data() {
    return {
      todo: "",
      todos: [],
    };
  },
  methods: {
    add() {
      const { todo } = this;
      this.todos.push({
        id: uuidv4(),
        todo,
        completed: false,
      });
      this.todo = "";
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>



