<template>
  <div class="container">
    <div id="app">
      <TodoBoard :todos="todos" @addTodo="addTodo" @deleteTodo="deleteTodo" @changeStatusTodo="changeStatusTodo" />
    </div>
  </div>
</template>

<script>
import TodoBoard from './components/TodoBoard.vue';

export default {
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
    deleteTodo(todoId) {
      this.todos = this.todos.filter(todo => todo.id !== todoId);
    },
    changeStatusTodo(todoId) {
      this.todos = this.todos.map(todo => {
        if (todo.id === todoId) {
          todo.completed = !todo.completed;
        }
        return todo;
      });
    },
  },
  components: {
    TodoBoard,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  justify-content: center;
}
.container {
  display: block;
  background-color: beige;
  width: 800px;
  height: 300px;
  box-shadow: transparent;
}
</style>
