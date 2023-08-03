<script>
import { defineNuxtComponent } from 'nuxt/app';
export default defineNuxtComponent({
  name: 'App',
  data: () => ({
    todoList: []
  }),
  computed: {
    completedTodo() {
      return this.todoList.filter(item => item.completed === true).length
    }
  },
  methods: {
    fetchTodoList() {
      fetch('https://jsonplaceholder.typicode.com/todos')
        .then(response => response.json())
        .then(json => {
          this.todoList = json
        })
    }
  }
});
</script>
<template>
  <div>
    <img src="/todo-img.jpg" alt="Todo photo" width="150px">
    <br>
    <button @click="fetchTodoList">Fetch TodoList</button>
    <!-- <pre>{{ todoList }}</pre> -->
    <p>Completed: {{ completedTodo }}</p>
    <ul>
      <li v-for="todo in todoList" :key="todo.id">
        <input type="checkbox" :checked="todo.completed">
        <span>{{ todo.title }}</span>
      </li>
    </ul>
  </div>
</template>
