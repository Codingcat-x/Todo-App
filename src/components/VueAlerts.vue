<template>
  <!-- <div class="alert alert-warning" role="alert">
    The input cannot be empty!
  </div> -->
  <div class="alert alert-warning alert-dismissible fade show" role="alert">
    <strong>Attention:</strong> The input cannot be empty!
    <button type="button" class="btn-close" @click="hide"></button>
  </div>
</template>

<script>
export default {
  name: 'VueAlerts',
  props: ['hideAlerts'],
  methods: {
    hide() {
      this.hideAlerts();
    }
  }
}
</script> 

<style scoped>
</style>