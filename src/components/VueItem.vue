<template>
  <div class="form-check">
    <input class="form-check-input" type="checkbox" value="" :checked="todo.completed" :id="todo.id"
    @click="handleCheck(todo.id)">
    <div class=" d-flex justify-content-between">
      <label class="form-check-label" :for="todo.id">
        {{ todo.text }}
      </label>
      <div class="button-group row gap-2">
        <!-- <button type="button" class="col btn btn-sm btn-outline-success">Edit</button> -->
        <button type="button" class="col btn btn-sm btn-outline-danger"
        @click="remove(todo.id)">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VueItem',
  props: ['todo', 'checkTodo', 'removeTodo'],
  methods: {
    handleCheck(id) {
      this.checkTodo(id);
    },
    remove(id) {
      this.removeTodo(id);
    }
  },
  mounted() {
  }
}
</script>

<style scoped>
.button-group {
  display: none;
}
.form-check:hover .button-group {
  display: flex;
}
.form-check {
  height: 30.6px;
}
.form-check:hover {
  height: auto;
}
.button-group {
  width: 110px;
  height: 30.6px;
}
.form-check-label {
  width: calc(100% - 110px);
  height: 30.6px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.form-check:hover .form-check-label {
  height: auto;
  /* overflow: auto; */
  white-space: wrap;
}
</style>