<template>
  <div>
    <form @submit.prevent="add">
      <input v-model="todo" />
      <button type="submit">Add</button>
    </form>
    <div v-for="(todo, index) of todos" :key="todo.id">
      <input type="checkbox" v-model="todo.completed" />
      <span :class="{ 'completed': todo.completed }">{{ todo.todo }}</span>
      <button @click="deleteTodo(index)">delete</button>
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
