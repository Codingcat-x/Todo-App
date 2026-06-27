<template>
  <div>
    <nav class="navbar navbar-expand-lg">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Todos</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Home</a>
            </li>
          </ul>
          <form class="d-flex form" role="search">
            <input class="form-control me-2" type="search" placeholder="Add a todo item and press enter" 
            aria-label="Search" @keyup.enter="addItem" v-model="text">
          </form>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import { nanoid } from 'nanoid';

export default {
  name: 'VueHeader',
  props: ['receive'],
  data() {
    return {
      text: '',
      isEmpty: false
    }
  },
  methods: {
    addItem() {
      if (this.text.trim() === '') {
        this.isEmpty = true;
      } else {
        this.isEmpty = false;
      }
      const obj = {
        id: nanoid(),
        text: this.text.trim(),
        completed: false
      }
      this.text = '';
      this.receive(obj, this.isEmpty);
    }
  }
}
</script>

<style scoped>
.form {
  width: 70%;
}
.form-control {
  width: 100%;
}
</style>