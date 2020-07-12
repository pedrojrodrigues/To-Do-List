<template>
  <div class="container">
    <div class="row justify-content-center">
      <p class="titulo display-3">To Do List</p>
    </div>
    <div class="row justify-content-center">
      <NewTodo @on-addtodo="addTodo($event)"/>
    </div>
    <div class="row justify-content-center">
      <div class="col-12 col-lg-6">
        <ul class="list-group">
          <Todo 
            v-for="(todo, index) in todos" 
            :key="index" 
            :todoString="todo.todoString"
            :completed="todo.completed"
            @on-delete="deleteTodo(todo)"
            @on-toggle="toggleTodo(todo)"
            @on-edit="editTodo(todo, $event)"
          />
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from "./Todo";
import NewTodo from "./NewTodo";
export default {
  components: {
    Todo,
    NewTodo
  }, 
  data() {
    return {
        todos: [
            { todoString: "Ex: item 1", completed: false },
        ]
    };
  },
  methods: {
    addTodo(newTodo) {
        this.todos.push({
            todoString: newTodo,
            completed: false
        });
    },
    toggleTodo(todo) {
        todo.completed = !todo.completed;
    },
    editTodo(todo, newTodoString) {
        todo.todoString = newTodoString;
    },
    deleteTodo(deleteTodo) {
        this.todos = this.todos.filter(todo => todo !== deleteTodo);
    }
  }
};
</script>

<style>
.titulo {
  color: aliceblue;
}
</style>