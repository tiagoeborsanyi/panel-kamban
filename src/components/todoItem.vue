<template>
  <div class="z-depth-3 todo-item" :style="colorido">
    <div class="content lmdd-block">
      <i class="material-icons handle">reorder</i>
      <a class="remove" @click="$emit('remove')"><i class="material-icons">clear</i></a>
      <div class="task">
        <p>{{dataitem}}</p>
        <!--i class="material-icons icon-color">more_horiz</i-->
        <div class="chip-tags">
          <div class="chip">
            <a href="#">@user</a>
          </div>
          <div class="chip" style="background-color:#0d9cfa" @click="editBlue">
            <p>.</p>
          </div>
          <div class="chip" style="background-color:#8bc34a" @click="editGreen">
            <p>.</p>
          </div>
          <div class="chip" style="background-color:#dcdcdc" @click="editBranco">
            <p>.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { eventItemColor } from '../main';

export default {
  data() {
    return {
      colorido: {background: '#8bc34a'}
    }
  },
  props: ['dataitem'],
  methods: {
    editBlue() {
      this.colorido = {background: '#0d9cfa'}
    },
    editGreen() {
      this.colorido = {background: '#8bc34a'}
    },
    editBranco() {
      this.colorido = {background: '#dcdcdc'}
    }
  }
}
</script>

<style lang="css">
.icon-color {
  margin-right: 5px;
  margin-bottom: 0;
  color: #ccc;
}

.chip-tags {
  display: inline-flex;
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

  .remove {
  color: red;
  float: right;
  cursor: pointer;
  }

  .task {
  border: 1px dotted white;
  padding: 5px;
  }
</style>
