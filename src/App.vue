<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-lg-3"></div>
        <div class="col-lg-6 col-sm-12">
          <VueHeader :receive="receive" :toggleTheme="toggleTheme" :isDark="isDark"/>
          <VueAlerts v-if="vueAlertsDisplay" :hideAlerts="hideAlerts" class="mt-2"/>
          <VueList v-if="todos.length > 0" :todos="todos" class="mt-2"
            :checkTodo="checkTodo" :removeTodo="removeTodo"/>
          <h3 class="mt-3 mb-3" v-else>
            There's no todo items yet.
          </h3>
          <VueFooter class="mt-2" v-show="todos.length > 0" 
            :todos="todos" :selectAll="selectAll" :clearCompleted="clearCompleted"/>
        </div>
        <div class="col-lg-3"></div>
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
      isDark: localStorage.getItem('theme') === 'dark',
    }
  },
  mounted() {
    // 页面加载时从 localStorage 读取主题偏好并应用到 <html>
    const theme = localStorage.getItem('theme');
    if (theme) {
      document.documentElement.setAttribute('data-bs-theme', theme);
    }
  },
  methods: {

    // 隐藏因为输入框为空时触发的警告框
    hideAlerts() {
      this.vueAlertsDisplay = false;
    },
    // 接收来自VueHeader组件的输入数据并接收输入框是否为空的isEmpty值
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
    selectAll(bool) {
      this.todos.forEach(todo => {
        todo.completed = bool;
      })
    },
    clearCompleted() {
      this.todos = this.todos.filter(todo => !todo.completed);
    },
    toggleTheme() {
      this.isDark = !this.isDark;
      const theme = this.isDark ? 'dark' : 'light';
      document.documentElement.setAttribute('data-bs-theme', theme);
      localStorage.setItem('theme', theme);
    }
  },
  watch: {
    todos: {
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
  color: var(--bs-body-color);
  margin-top: 20px;
}
h3 {
  text-align: center;
}
</style>
