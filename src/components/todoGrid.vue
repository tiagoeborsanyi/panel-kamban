<template>
  <div id="drag-scope">
    <div class="column" v-for="(t, index) in todos">
      <div class="title">{{t.title}}</div>
      <todo-container class="regular lighten-5" :class="colors.verde" :data="t.regular">
        <todo-item
          v-for="(todo, i) in t.regular"
          :dataitem="todo"
          :key="i"
          @remove="t.regular.splice(i, 1)"></todo-item>
          <div class="input-model">
            <input type="text" placeholder="Insira uma task" :id="index" @keyup.enter="insertItem(index)">
          </div>
      </todo-container>
    </div>
  </div>
</template>

<script>
import todoContainer from './todoContainer.vue';
import todoItem from './todoItem.vue';
export default {
  data() {
    return {
      item: '',
      colors: {
        verde: 'green',
        azul: 'blue',
        laranja: 'orange',
        cinza: '#3e3e3e',
        purpura: '#b035fb',
        vermelho: 'red',
        ceu: '#3cfad8'
      }
    }
  },
  props: ['todos'],
  components: {
    todoContainer,
    todoItem
  },
  methods: {
    insertItem (index) {
      this.$emit('addItemList', [index, document.getElementById(index).value]);
      console.log(document.getElementById(index).value);
      document.getElementById(index).value = ''
    }
  }
}
</script>

<style>
</style>
