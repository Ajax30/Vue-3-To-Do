<template>
  <footer>
    <form @submit.prevent="addTodo()">
      <input type="text" :placeholder="placeholder" v-model="newTitle">
      <span class="error" v-if="!isValidInput">{{validationMsg}}</span>
    </form>
  </footer>
</template>

<script>
export default {
  name: 'Footer',

  props: {
    placeholder: String,
    validationMsg: String,
    isValidInput: Boolean
  },

  data () {
    return {
     newTitle: '',
    }
  },

  methods: {
    addTodo() {
      this.$emit('add-todo', this.newTitle)
      this.newTitle = ''
    }
  }
}
</script>

<style scoped>
  footer {
    padding: 15px 20px 25px 20px;
    margin-top: auto;
    position: relative;
  }

  .error {
    position: absolute;
    top: 5px;
    right: 22px;
    font-size: 11px;
    color: #c00;
  }

  input[type="text"] {
    width: 100%;
    padding: 2px 4px;
    border: none;
    font-size: 16px;
    outline: none;
    border-bottom: 2px solid #b8b8b8;
    transition: border-bottom 200ms ease-in;
  }

  input[type="text"]:focus {
    border-bottom: 2px solid #dddddd;
  }
</style>
