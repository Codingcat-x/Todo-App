<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-3"></div>
        <div class="col-6">
          <VueHeader :receive="receive"/>
          <VueAlerts v-if="vueAlertsDisplay" :hideAlerts="hideAlerts" class="mt-2"/>
          <VueList v-if="todos.length > 0" :todos="todos" class="mt-2"
            :checkTodo="checkTodo" :removeTodo="removeTodo"/>
          <h3 class="mt-3 mb-3" v-else>
            There's no todo items yet.
          </h3>
          <VueFooter class="mt-2" v-show="todos.length > 0" 
            :todos="todos" :selectAll="selectAll" :clearCompleted="clearCompleted"/>
        </div>
        <div class="col-3"></div>
      </div>
    </div>
  </div>
</template>

<script>
import VueHeader from './components/VueHeader.vue';
import VueList from './components/VueList.vue';
import VueFooter from './components/VueFooter.vue';
import VueAlerts from './components/VueAlerts.vue';

export default {
  name: 'App',
  components: { VueHeader, VueList, VueFooter, VueAlerts },
  data() {
    return {
      vueAlertsDisplay: false,
      todos: JSON.parse(localStorage.getItem('todos')) || [],
    }
  },
  methods: {
    // 隐藏因为输入框为空时触发的警告框
    // Hide alerts when input is empty
    hideAlerts() {
      this.vueAlertsDisplay = false;
    },
    // 接收来自VueHeader组件的输入数据并接收输入框是否为空的isEmpty值
    // Receive data from VueHeader component and receive isEmpty value
    receive(data, isEmpty) {
      if (isEmpty) return this.vueAlertsDisplay = true;
      this.todos.unshift(data);
      this.vueAlertsDisplay = false;
    },
    checkTodo(id) {
      this.todos.forEach( todo => {
        if (todo.id === id) todo.completed = !todo.completed;
      })
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    // 全选所有的Todo
    // Select all todos
    selectAll(bool) {
      this.todos.forEach(todo => {
        todo.completed = bool;
      })
    },
    // 清除所有已完成的Todo
    // Clear completed todos
    clearCompleted() {
      this.todos = this.todos.filter(todo => !todo.completed);
    }
  },
  watch: {
    todos: {
      // 开启深度监视
      // Open deep watching
      deep: true,
      handler(value) {
        localStorage.setItem('todos', JSON.stringify(value));
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 20px;
}
h3 {
  text-align: center;
}
</style>
