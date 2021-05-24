<template>
  <transition-group name="list" tag="ul" class="todo-list" v-if=dataIsLoaded>
      <TodoItem v-for="(todo, index) in todos.slice().reverse()"
        :key="todo.id" 
        :class="{done: todo.completed, active: index == 0}" 
        :todo="todo" 
        @delete-todo="$emit('delete-todo', todo.id)"
        @toggle-todo="$emit('toggle-todo', todo)"
        />
    </transition-group>
    <div class="loader" v-else></div>   
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  name: 'List',

  components: {
    TodoItem,
  },

  props: {
    dataIsLoaded: Boolean,
    todos: Array
  },

  emits: [
    'delete-todo',
    'toggle-todo'
  ]
}
</script>
  
<style scoped>
  .todo-list {
    flex: 1;
    overflow-y: auto;
    list-style-type: none;
    padding: 15px 20px 5px 20px;
    color: #4f4f4f;
  }

  ::-webkit-scrollbar {
    width: 5px;
  }

  ::-webkit-scrollbar-track {
    background: #efefef;
  }

  ::-webkit-scrollbar-thumb {
    background: #d0d0d0;
  }

  ::-webkit-scrollbar-thumb:hover {
    background: #d0d0d0;
  }

  .loader {
    border: 4px solid #ccc;
    border-top-color: transparent;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    position: absolute;
    top: 50%;
    margin-left: -25px;
    left: 50%;
    margin-top: -25px;
    animation: spin 2s linear infinite;
  }

  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
</style>
