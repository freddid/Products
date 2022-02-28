<template>
  <div id="app">
    <div class="sidebar">
      <AddProduct />
    </div>
    <div class="content">
      <Products />
    </div>
  </div>
</template>

<script>

export default {
  mounted () {
    this.$store.commit('productsData/getProduct')
  },
  created () {
    this.$store.subscribe((mutation, state) => {
      localStorage.setItem('products', JSON.stringify(state.productsData.products))
    })
  }
}
</script>

<style scoped>
#app {
  padding: 32px;
  display: flex;
}
#app .sidebar {
  min-width: 332px;
  max-width: 30%;
}
#app .content {
  width: 100%;
}
</style>
