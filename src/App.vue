<template>
  <div class="container">
    <p class="text-center">Todo App</p>
    <form @submit.prevent="addTodo">
      <div class="mb-3">
        <label for="exampleTodo" class="form-label">New Todo</label>
        <input
          type="text"
          class="form-control"
          id="exampleTodo"
          aria-describedby="newTodoHelp"
          v-model="newTodo"
        />
        <div id="newTodoHelp" class="form-text">Ender a new todo</div>
      </div>
      <button type="submit" class="btn btn-primary">Add Todo</button>
    </form>

    <ul class="list-group mt-3">
      <li
        v-for="(todo,i) in todos"
        :class="['list-group-item', { done: todo.completed }]"
        :key="todo"
      >
        <span class="float-start ">{{ todo.title }} </span>
        <button
          v-if="!todo.completed"
          class="btn btn-primary btn-sm float-end ms-1"
          @click="markDone(todo)"
        >
          done
        </button>
        <button
          class="btn btn-danger btn-sm float-end"
          @click="deleteTodo(i)"
        >
          delete
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: null,
      todos: [],
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        title: this.newTodo,
        completed: false,
      });
      this.newTodo = "";
  
    },
    markDone(todo) {
      todo.completed = !todo.completed;
    },
    deleteTodo(i) {

        this.todos.splice(i, 1);

    },

  }, 
  watch: {
      todos:{
          handler() {
              localStorage.todos =  JSON.stringify(this.todos)
        },
        deep : true
      }
  },
  mounted() {
      if(localStorage.todos){
          this.todos = JSON.parse(localStorage.todos)
      }
  }
};
</script>

<style>
.done {
  background: #f03;
}
</style>
