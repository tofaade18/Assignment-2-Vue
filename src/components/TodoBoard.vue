<template>
    <div>
      <form @submit.prevent="handleAddTodo">
        <input v-model="newTodo" placeholder="Add a new todo" class="i-todo" />
        <input type="date" v-model="selectedDate" />
        <button class="btn btn-primary">Add</button>
      </form>
      <TodoItems :todos="todos" @deleteTodo="deleteTodo" @changeStatusTodo="changeStatusTodo" />
    </div>
  </template>
  
  <script>
  import TodoItems from './TodoItems.vue';
  
  export default {
    props: ['todos'],
    data() {
      return {
        newTodo: '',
        selectedDate: '',
      };
    },
    methods: {
      handleAddTodo() {
        if (this.newTodo.trim() !== '') {
            const currentDate = new Date().toLocaleDateString();
            const todo = {
                id: Date.now(),
                text: this.newTodo,
                completed: false,
                date: this.selectedDate || null, // Use the selected date or null if not provided
                dateNow: currentDate,
                }
            this.$emit('addTodo', todo);
            this.newTodo = '';
            this.selectedDate = '';
        //   this.$emit('addTodo', { id: Date.now(), text: this.newTodo, completed: false });
        //   this.newTodo = '';
        }
      },
      deleteTodo(todoId) {
        this.$emit('deleteTodo', todoId);
      },
      changeStatusTodo(todoId) {
        this.$emit('changeStatusTodo', todoId);
      },
    },
    components: {
      TodoItems,
    },
  };
  </script>
  
<style scoped>
.btn {
    background-color: blue;
    color: white;
    border-radius: 9rem;
    width: 90px;
    height: 40px;
    margin-left: 10px;
}
.i-todo {
    margin-right: 20px;
    display: inline;
    width: 500px;
    height: 40px;
    line-height: 2em ;
}
</style>