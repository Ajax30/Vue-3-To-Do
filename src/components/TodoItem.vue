<template>
  <li>
    <input type="checkbox" :checked="todo.completed" @change="$emit('toggle-todo', todo)" />
    <span class="title">{{todo.title}}</span>
    <button @click="$emit('delete-todo', todo.id)">
      <i class="fas fa-trash-alt"></i>
    </button>
 </li>
</template>

<script>

export default {
  name: 'TodoItem',

  props: {
    todo: Object
  }
}
</script>

<style scoped>
  li {
    position: relative;
    display: flex;
    overflow: hidden;
    align-items: center;
    font-size: 13px;
    padding: 10px;
    cursor: pointer;
    margin-bottom: 7px;
    border: 1px solid rgba(0, 0, 0, 0.07);
    background: #d4e7f7;
    border-radius: 2px;
    transition: all 0.3s ease; 
  }

  li:last-child {
    margin-bottom: 0;
  }

  .list-enter-active, .list-leave-active {
    transition: all .5s;
  }

  .list-enter, .list-leave-to {
    opacity: 0;
    transform: translateX(-295px);
  }

  .done {
    text-decoration: line-through;
  }

  input[type="checkbox"] {
    display: block;
    margin-bottom: -1px;
    margin-right: 7px;
  }

  button {
    border: none;
    background: #c00;
    color: #fff;
    cursor: pointer;
    position: absolute;
    z-index: 1;
    top: -1px;
    bottom: -1px;
    right: -1px;
    font-size: 18px;
    width: 50px;
    transform: translateX(50px);
    transition: transform 200ms;
  }

  .todo-list li:hover button {
    transform: translateX(0);
  }
</style>
