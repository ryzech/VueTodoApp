<script setup>
import { useDark, useToggle } from "@vueuse/core";

const isDark = useDark({ 
  selector: "body", //element to add attribute to
  attribute: "theme", // attribute name
  valueDark: "custom-dark", // attribute value for dark mode
  valueLight: "custom-light", // attribute value for light mode
});
const toggleDark = useToggle(isDark);
</script>

<template>
  <div class="container">
    <button @click="toggleDark()">
      Toggle Color Mode
    </button>
    <h2>{{ title }}</h2>
    <form @submit.prevent="addTodo">
      <label for="newTodo" class="todoLabel">New Todo</label>
      <input v-model="newTodo" type="text" name="newTodo" id="newTodo" class="newTodo" />
      <button type="submit" name="button" class="addNew">Add</button>
    </form>
    <li v-for="todo in todos" :key="todo.title" class="todoList">
      <input type="checkbox" name="done" v-model="todo.done" class="checkbox"/>
      <span :class="{ done: todo.done }">{{ todo.title }}</span>
      <button @click="removeTodo(todo)" type="button" class="remove">Remove</button>
    </li>
    <button @click="markAllDone" type="button" class="allDone">Mark All Done</button>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      title: 'Todo List',
      newTodo: '',
      todos: []
    }
  },
  methods: {
    addTodo() {
      this.todos.push({
        title: this.newTodo,
        done: false
      })
      this.newTodo = ''
    },
    removeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo)
      this.todos.splice(todoIndex, 1)
    },
    markAllDone() {
      this.todos.forEach((todo) => {
        todo.done = true
      })
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Kanit&display=swap');
@import '../assets/base.css';
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: 'Kanit', sans-serif;
}
button {
  padding: 0.5rem 1.5rem;
  font-size: 1rem;
  border: none;
  cursor: pointer;
  border-radius: 50px;
}
h2 {
  font-size: 3.5rem;
  color: black;
}
.newTodo{
  padding: 0.5rem 1.5rem;
  margin: 0 10px 0 10px;
  font-size: 1rem;
  border: none;
  cursor: pointer;
  border-radius: 50px;
  outline: 2px dashed black;
}
.done {
  text-decoration: line-through;
}
.container {
    width: 40%;
    top: 50%;
    left: 50%;
    background: white;
    border-radius: 10px;
    min-width: 450px;
    position: absolute;
    min-height: 100px;
    transform: translate(-50%,-50%);
    text-align: center;
}
.todoList {
  list-style-type: none;
  margin: 0;
  padding: 0;
  font-size: 1.5rem;
  color: black;
  display:flex;
  justify-content:space-between;
}
.todoLabel {
  color: black;
}
.allDone {
  margin-top: 6px;
  padding-top: 6px;
  margin-bottom: 5px;
}
.remove {
  text-align: right;
  margin-left: 315px;
  display:flex;
  justify-content:space-between;
}
.checkbox {
  margin-left: 5px;
}
.addNew {
  
}

[theme="custom-dark"] {
  background: #16171d; 
  color: #fff;
}

[theme="custom-light"] {
  background: white;
  color: #16171d;
}
</style>
