<template>
  <div>
    <h2>Todo application</h2>
    <router-link to="/">home</router-link>
    <hr>
    <AddTodo 
      @add-todo="addTodo"
    />
    <hr>
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not-completed</option>
    </select>
    <hr> 
    <Loader  v-if="loading" />
    <TodoList
      v-else-if="fileredTodos.length"
      v-bind:todos="fileredTodos"
      @remove-todo="removeTodo"
    />
    <p v-else>no todos!</p>
  </div> 
</template>

<script>
import TodoList from '@/components/TodoList'
import Loader from '@/components/loader'
import AddTodo from '@/components/AddTodo'
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all',
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
        this.todos = json
        this.loading = false
      })
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  },
  // watch: {
  //   filter(value) {
  //     console.log(value);
  //   }
  // },
  computed: {
    // eslint-disable-next-line vue/return-in-computed-property
    fileredTodos() {
      if (this.filter === 'all') {
        return this.todos;
      }

      if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed);
      }

      if (this.filter === 'not-completed') {
        return this.todos.filter(t => !t.completed);
      }
    }
  },
  methods: {
      removeTodo(id) {
          this.todos = this.todos.filter(t => t.id !== id)
      },
      addTodo(todo) {
        this.todos.push(todo)
      }
  }
}
</script>