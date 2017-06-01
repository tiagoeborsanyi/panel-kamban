<template>
  <div id="app">
    <div class="input-model">
      <input v-model="newTodoText" @keyup.enter="addNewTodo" placeholder="Adicione uma nova task">
    </div>
    <div id="drag-scope">
      <div class="column">
        <div class="title">Tarefas a Fazer</div>
        <todo-container class="regular green lighten-5" :data="todos.regular">
          <todo-item
            v-for="(todo, index) in todos.regular"
            :dataitem="todo"
            :key="index"
            @remove="todos.regular.splice(index, 1)"></todo-item>
        </todo-container>
      </div>
      <div class="column">
        <div class="title">Em Andamento</div>
        <todo-container class="priority red lighten-4" :data="todos.priority">
          <todo-item
            v-for="(todo, index) in todos.priority"
            :dataitem="todo"
            :key="index"
            @remove="todos.priority.splice(index, 1)"></todo-item>
        </todo-container>
      </div>
      <div class="column">
        <div class="title">Concluido</div>
        <todo-container class="done grey lighten-2" :data="todos.done">
          <todo-item
            v-for="(todo, index) in todos.done"
            :dataitem="todo"
            :key="index"
            @remove="todos.done.splice(index, 1)"></todo-item>
        </todo-container>
      </div>
    </div>
  </div>
</template>

<script>
import todoContainer from './components/todoContainer.vue';
import todoItem from './components/todoItem.vue';

export default {
  data () {
    return {
      newTodoText: '',
      todos: {
        regular: [
          'Inicio do Projeto',
          'Commit inicial',
          'Execução do Projeto'
        ],
        priority: [],
        done: []
      }
    }
  },
  components: {
    todoContainer,
    todoItem
  },
  mounted() {
    lmdd.set(document.getElementById('drag-scope'), {
      containerClass: 'todo-container',
      draggableItemClass: 'todo-item',
      handleClass: 'handle',
      dataMode: true
    });
    this.$el.addEventListener('lmddend', this.handleDragEvent);
  },
  methods: {
    handleDragEvent(event) {
      console.log(event);
      var newIndex = event.detail.to.index;
      var oldIndex = event.detail.from.index;
      var newContainer = event.detail.to.container.__vue__.data;
      var oldContainer = event.detail.from.container.__vue__.data;
      if (event.detail.dragType === 'move') {
        newContainer.splice(newIndex, 0, oldContainer.splice(oldIndex, 1)[0]);
      }
    },
    addNewTodo() {
      this.todos.regular.push(this.newTodoText)
      this.newTodoText = ''
    }
  }
}
</script>

<style>
  #app {
    width: 100%;
    margin-top: 15px;
    margin-bottom: 15px;
    }

  #drag-scope {
    display: flex;
    justify-content: space-around;
    background-color: white;
    }

    .column {
      flex: 1 1 350px;
      }

    .todo-container {
      display: flex;
      padding: 10px;
      margin: 5px;
      flex-flow: column nowrap;
      min-height: 106px;
    }

    .todo-item {
    padding: 3px;
    margin: 5px;
    color: black;
    font-size: 15px;
    background-color: grey;
    border: 3px solid lightgoldenrodyellow;
    }

    .regular .todo-item {
      background-color: #8bc34a;
    }

    .priority .todo-item {
      background-color: #E57373;
    }

    .done .todo-item {
      background-color: lightgrey;
      color: gray;
      text-decoration: line-through;
    }

    .handle {
      cursor: move;
    }

  .title {
    text-align: center;
    font-weight: bold;
    padding: 10px;
    margin: 5px;
    }

  .input-model {
    padding: 0px 30px;
    }
</style>
