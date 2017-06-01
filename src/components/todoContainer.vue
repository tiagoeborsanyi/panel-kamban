<template>
  <div class="todo-container">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: ['data']
}
</script>

<style escoped>
.todo-container {
  display: flex;
  padding: 10px;
  margin: 10px;
  flex-flow: column nowrap;
  min-height: 106px;
  }
</style>
