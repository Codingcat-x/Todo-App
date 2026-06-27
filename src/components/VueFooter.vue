<template>
  <div class="card">
    <div class="card-body">
      <div class="form-check">
        <input class="form-check-input" type="checkbox" value="" id="CheckAll"
          v-model="isCheckAll">
        <div class=" d-flex justify-content-between">
          <label class="form-check-label" for="CheckAll">
            Completed {{ completed }} / All {{ total }}
          </label>
          <div class="button-group">
            <button type="button" class="col btn btn-sm btn-outline-danger"
              @click="clearAll">Clear all completed</button>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: 'VueFooter',
  props: ['todos', 'selectAll', 'clearCompleted'],
  data() {
    return {
    }
  },
  methods: {
    checkAll(e) {
      this.selectAll(e.target.checked);
    },
    clearAll() {
      this.clearCompleted();
    }
  },
  computed: {
    completed() {
      return this.todos.reduce((acc, todo) => acc + (todo.completed ? 1 : 0), 0);
    },
    total() {
      return this.todos.length;
    },
    isCheckAll: {
      get() {
        return this.completed === this.total && this.total > 0;
      },
      set(value) { 
        this.selectAll(value);
      }
    }
  }
}
</script>

<style scoped>
</style>