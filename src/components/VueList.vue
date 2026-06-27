<template>
  <div>
    <div class="card ">
      <div class="card-body">
        <div class="list-group  list-group-flush">
          <!-- <li class="list-group-item bg-secondary-subtle" v-for="todo in todos" :key="todo.id">
            <VueItem :todo="todo" :checkTodo="checkTodo"></VueItem>
          </li> -->
          <a href="#" class="list-group-item list-group-item-action"
           v-for="todo in todos" :key="todo.id">
            <VueItem :todo="todo" :checkTodo="checkTodo" :removeTodo="removeTodo"></VueItem>
          </a>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import VueItem from './VueItem.vue'

export default {
  name: 'VueList',
  components: { VueItem },
  props: ['todos', 'checkTodo', 'removeTodo'],
  data() {
    return {
      
    }
  }
}
</script>

<style scoped>
.list-group {
  max-height: calc(100vh - 220px);
  overflow-y: auto;
}
.list-group::-webkit-scrollbar {
  width: 0.4rem;
}
.list-group::-webkit-scrollbar-thumb {
  background-color: #8888888a;
  border-radius: 5px;
}
</style>