<template>
    <div class="todo-list">
      <h1>TO DO List</h1>
      <input v-model="newTask.title" placeholder="Enter a task" />
      <input v-model="newTask.description" placeholder="Enter description" />
      <button @click="addTask">Add Task</button>
  
      <div v-for="todo in todos" :key="todo.id">
        <TodoItem 
          :identifier="todo.id" 
          :title="todo.title" 
          :description="todo.description"
          @edit-task="editTask"
          @delete-task="deleteTask" />
      </div>
    </div>
  </template>
  
  <script>
  import TodoItem from './TodoItem.vue';
  
  export default {
    name: "TodoList",
    components: {
      TodoItem
    },
    data() {
      return {
        newTask: {
          title: '',
          description: ''
        },
        todos: []
      };
    },
    methods: {
      addTask() {
        if (this.newTask.title && this.newTask.description) {
          const newId = 'Task-' + (this.todos.length + 1);
          this.todos.push({ id: newId, title: this.newTask.title, description: this.newTask.description });
          this.newTask.title = '';
          this.newTask.description = '';
        }
      },
      editTask(id) {
        const task = this.todos.find(todo => todo.id === id);
        if (task) {
          this.newTask.title = task.title;
          this.newTask.description = task.description;
          this.todos = this.todos.filter(todo => todo.id !== id);
        }
      },
      deleteTask(id) {
        this.todos = this.todos.filter(todo => todo.id !== id);
      }
    },
    created() {
      console.log('TodoList component created');
    }
  }
  </script>
  
  <style scoped>
  .todo-list {
    max-width: 400px;
    margin: 0 auto;
    text-align: center;
  }
  input {
    display: block;
    margin: 10px auto;
    padding: 5px;
    width: 80%;
  }
  button {
    background-color: #6c63ff;
    color: white;
    border: none;
    border-radius: 3px;
    padding: 5px 10px;
    cursor: pointer;
  }
  button:hover {
    background-color: #4b47db;
  }
  </style>
  