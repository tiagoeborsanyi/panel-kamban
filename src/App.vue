<template>
  <div id="app">
    <div class="input-model">
      Add a list:
      <input v-model="newTodoList" @keyup.enter="addNewList" placeholder="Adicione uma nova coluna">
    </div>
    <div id="drag-scope">
      <todo-grid :todos="todos" @addItemList="addItem"></todo-grid>
    </div>
  </div>
</template>

<script>
import todoGrid from './components/todoGrid.vue';
export default {
  data () {
    return {
      newTodoList: '',
      todos: [
        /*{
          title: 'teste regular',
          regular: [
            'Inicio do Projeto',
            'Commit inicial',
            'Execução do Projeto'
          ]
        }*/
      ]
    }
  },
  components: {
    todoGrid
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
    },
    addNewList() {
      this.todos.push({
        title: this.newTodoList,
        regular: []
      })
    },
    addItem (value) {
      this.todos[value[0]].regular.push(value[1]);
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

    .bloco {
      display: inline-flex;
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
