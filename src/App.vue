<template>
  <div id="app">
    <Header 
    title="My todo list" 
    :unsolvedTodos = []
    />

    <List 
      :todos="todos"
      dataIsLoaded=false 
      @delete-todo="deleteTodo" 
      @toggle-todo="toggleTodo" />

    <Footer
      :isValidInput = true
      newTitle = ""
      placeholder="+ Add new todo"
      validationMsg = "Please add at least 3 characters"
      @add-todo="addTodo"
      />

  </div>
</template>

<script>
import axios from 'axios'
import Header from './components/Header.vue'
import List from './components/List.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    List,
    Footer
  },

  data() {
    return {
      url: "https://jsonplaceholder.typicode.com/todos?&_limit=5",
      dataIsLoaded: false,
      isValidInput: true,
      todos: [],
      unsolvedTodos: [],
    }
  },

  mounted() {
    axios.get(this.url)
      .then((response) => {
        this.todos = response.data;
      })
     .then(this.getUnsolvedTodos);
      this.dataIsLoaded = true;
  },

  methods: {
    getUnsolvedTodos: function(){
      this.unsolvedTodos = this.todos.filter(todo => {
        return todo.completed === false;
      });
    },

    toggleTodo: function(todo) {
      todo.completed = !todo.completed;
      this.getUnsolvedTodos();
    },

    deleteTodo: function(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
      this.getUnsolvedTodos();
    },

    addTodo: function(newTitle){
     let lastId = this.todos.length === 0 ? 0 : this.todos[this.todos.length - 1].id;
     const newToDo = {
        id: lastId + 1,
        title: newTitle,
        completed: false
      }
     
      if(newTitle.length > 2){
        this.isValidInput = true;
        this.todos.push(newToDo);
      } else {
        this.isValidInput = false;
      }
      
      this.getUnsolvedTodos();
    }
  },

  watch: {
    
  }
}

</script>

<style>
#app {
  width: 320px;
  height: 320px;
  display: flex;
  flex-direction: column;
  background: #fff;
  box-shadow: rgb(99 99 99 / 20%) 0px 2px 8px 0px;
  overflow: hidden;
  border-radius: 8px;
  position: relative;
}
</style>
