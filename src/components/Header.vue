<template>
  <header>
    <span class="title">{{title}}</span>
    <span class="count" :class="{zero: unsolvedTodos.length === 0}">{{unsolvedTodos.length}}</span>
  </header>
</template>

<script>
export default {
  props: {
    title: String,
    unsolvedTodos: Array
  },
}
</script>

<style scoped>
  header {
    padding: 15px 20px;
    background: #efefef;
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
    font-size: 18px;
    font-weight: 600;
    display: flex;
  }

  .title {
    font-size: 18px;
    font-weight: 600;
    color: #323232;
  }

  .count {
    margin-left: auto;
    display: inline-block;
    width: 26px;
    line-height: 26px;
    text-align: center;
    border-radius: 3px;
    font-size: 13px;
    background: #c00;
    color: #fff;
  }

  .count.zero {
    background: #009688;
  }
</style>
