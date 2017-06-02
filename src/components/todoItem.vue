<template>
  <div class="z-depth-3 todo-item">
    <div class="content lmdd-block">
      <i class="material-icons handle">reorder</i>
      <a class="remove" @click="$emit('remove')"><i class="material-icons">clear</i></a>
      <div class="task">
        <p>{{dataitem}}</p>
        <!--i class="material-icons icon-color">more_horiz</i-->
        <div class="chip">
          <a href="#">@user</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['dataitem']
}
</script>

<style lang="css">
.icon-color {
  margin-right: 5px;
  margin-bottom: 0;
  color: #ccc;
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
