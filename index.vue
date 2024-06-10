<template>
  <div>
    <h1>Todo List</h1>
    <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add a new todo" />
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" v-model="todo.done" />
        <span :style="{ textDecoration: todo.done ? 'line-through' : 'none' }">{{ todo.text }}</span>
        <button @click="removeTodo(index)">Remove</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

interface Todo {
  text: string;
  done: boolean;
}

export default defineComponent({
  data() {
    return {
      newTodo: '',
      todos: [] as Todo[]
    };
  },
  mounted() {
    const savedTodos = localStorage.getItem('todos');
    if (savedTodos) {
      this.todos = JSON.parse(savedTodos);
    }
  },
  watch: {
    todos: {
      handler(newTodos: Todo[]) {
        localStorage.setItem('todos', JSON.stringify(newTodos));
      },
      deep: true
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo, done: false });
        this.newTodo = '';
      }
    },
    removeTodo(index: number) {
      this.todos.splice(index, 1);
    }
  }
});
</script>

<style>
/* スタイルは必要に応じて追加してください */
</style>