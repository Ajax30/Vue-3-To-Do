<template>
  <div id="app">
    <Header 
    title="My todo list" 
    :unsolvedTodos = unsolvedTodos
    />

    <List 
      :todos="todos"
      :dataIsLoaded=dataIsLoaded
      @delete-todo="deleteTodo" 
      @toggle-todo="toggleTodo" />

    <Footer
      :isValidInput=isValidInput
      newTitle = ""
      placeholder= "+ Add new todo"
      validationMsg = "Please add at least 3 characters"
      @add-todo="addTodo"
      />

  </div>
</template>

<script>
import axios from 'axios'
import '@fortawesome/fontawesome-free/js/all.js';
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
      apiUrl: "http://todo.com/api",
      dataIsLoaded: false,
      isValidInput: true,
      todos: [],
      unsolvedTodos: [],
    }
  },

  methods: {
    showTodos: function(){
      axios.get(`${this.apiUrl}/todos`)
      .then((response) => {
        this.todos = response.data;
      })
     .then(this.getUnsolvedTodos)
     .then(this.dataIsLoaded = true);
    },

    getUnsolvedTodos: function(){
      this.unsolvedTodos = this.todos.filter(todo => {
        return todo.completed == 0;
      });
    },

    toggleTodo: function(todo) {
      let newStatus = todo.completed == "0" ? 1 : 0;
      axios.put(`${this.apiUrl}/todo/update/${todo.id}`, {
        title: todo.title,
        completed: newStatus
      })
    },

    deleteTodo: function(id) {
      axios.delete(`${this.apiUrl}/todo/delete/${id}`)
    },

    addTodo: function(newTitle){
     const newToDo = {
        title: newTitle,
        completed: 0
      }
     
      if(newTitle.length > 2){
        this.isValidInput = true;
        axios.post(`${this.apiUrl}/todo/add`, newToDo);
      } else {
        this.isValidInput = false;
      }
    }
  },

  created() {
    this.showTodos();
  },

  watch: {
    todos() {
      this.showTodos();
    }
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
