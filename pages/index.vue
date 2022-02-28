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
}
</script>

<style scoped>
#app{
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
