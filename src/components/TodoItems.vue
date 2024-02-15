<template>
    <ul>
      <li class="list" v-for="todo in todos" :key="todo.id">
        <div>
            <input type="checkbox" class="checked" :checked="todo.completed" @change="changeStatusTodo(todo.id)" />
            <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
            <span v-if="todo.date" class="date">Deadline: {{ todo.date }}</span>
            <span v-if="todo.dateNow" class="date-now">Added on: {{ todo.dateNow }}</span>
            <span @click="deleteTodo(todo.id)" class="delete-icon">&#128465;</span>
        </div>
      </li>
    </ul>
  </template>
  
  <script>
  export default {
    props: ['todos'],
    methods: {
      deleteTodo(todoId) {
        this.$emit('deleteTodo', todoId);
      },
      changeStatusTodo(todoId) {
        this.$emit('changeStatusTodo', todoId);
      },
    },
  };
  </script>
  
  <style scoped>
  .checked {
    margin-right: 40px;
    display: flexbox;
    align-items:flex-start;
  }
  .completed {
    text-align: start;
    margin-left: 10px;
  }
  .date {
  margin-left: 10px;
  color: black;
  font-weight: bold;
  }
  .date-now {
  margin-left: 10px;
  color: #555;}
  .delete-icon {
  cursor: pointer;
  color: #e74c3c;
  margin-left: 10px;
  font-size: x-large;
  background-color:snow;}
  </style>
  