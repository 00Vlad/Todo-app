<template>
  <div id="app">
    <span>Todo Application</span>
    <hr>
    <AddTodo
      @add-todo='addTodo'
    />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
    <hr>
    <Loader v-if="loading"/>
    <TodoList 
      v-else-if="filteredTodos.length"
      :todos='filteredTodos'
      @remove-todo='removeTodo'
    />
    <p v-else>No todos</p>
  </div>
</template>



<script>
import TodoList from '@/components/TodoList.vue'
import AddTodo from '@/components/AddTodo.vue'
import Loader from '@/components/Loader.vue'

export default {
  name: 'App',
  components: {
    TodoList, AddTodo, Loader
  },

  data() {
    return {
      todos: [],
      loading: true,
      filter: 'not-completed'
    }
  },

  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
          this.todos = json
          this.loading = false
        }, 500)
      })
  },
  computed: {
    filteredTodos() {
      switch (this.filter) {
        case 'all':
          return this.todos

        case 'completed':
          return this.todos.filter(el => el.completed)
        
        case 'not-completed':
          return this.todos.filter(el => !el.completed)
      }
      return 'all'
    }
  },

  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter((el) =>el.id !== id)
    },
    addTodo(newTodo) {
      this.todos.push(newTodo)
    }
  }
}
</script>



<style scoped>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 60px;
    text-align: center;
}
  span {
    display: block;
    font-size: 1.4rem;
    font-weight: 700;
    margin-bottom: 1.5rem;
  }
  select {
    margin-top: .6rem;
  }
  hr {
    margin-bottom: 1.5rem;
  }
</style>