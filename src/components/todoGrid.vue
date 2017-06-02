<template>
  <div class="bloco">
    <div class="column" v-for="t in todos">
      <div class="title">{{t.title}}</div>
      <todo-container class="regular green lighten-5" :data="t.regular">
        <todo-item
          v-for="(todo, index) in t.regular"
          :dataitem="todo"
          :key="index"
          @remove="t.regular.splice(index, 1)"></todo-item>
          <div class="input-model">
            <input type="text" placeholder="Insira uma task" @click="insertItem">
          </div>
      </todo-container>
    </div>
  </div>
</template>

<script>
import todoContainer from './todoContainer.vue';
import todoItem from './todoItem.vue';
export default {
  props: ['todos'],
  components: {
    todoContainer,
    todoItem
  },
  methods: {
    insertItem () {
      
    }
  }
}
</script>

<style>
</style>
