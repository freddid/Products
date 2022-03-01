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
      localStorage.setItem(
        'products',
        JSON.stringify(state.productsData.products)
      )
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
}
#app .content {
  width: 100%;
}

@media (max-width: 720px) {
  #app {
    flex-wrap: wrap;
    justify-content: center;
  }
}

@media (max-width: 480px) {
  #app {
    padding: 15px;
  }
  #app .sidebar {
    min-width: unset;
    width: 100%;
  }
}
</style>
