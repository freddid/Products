<template>
  <div class="products">
    <header class="products__header">
      <ProductsFilter @selectOption="sortProdutcts" />
    </header>
    <div class="product__cards">
      <ProductsCards
        :src="product.urlImg"
        :price="+product.price"
        :title="product.name"
        :txt="product.descript"
        :id="product.id"
        @removeProduct="removeProduct"
        v-for="product in products"
        :key="product.id"
      />
    </div>
  </div>
</template>
<script>
import ProductsFilter from '@/components/Products/ProductsFilter.vue'
import ProductsCards from '~/components/Products/ProductsCard.vue'
import { mapGetters, mapMutations } from 'vuex'
export default {
  components: {
    ProductsFilter,
    ProductsCards
  },
  computed: {
    ...mapGetters('productsData', ['products'])
  },
  methods: {
    ...mapMutations('productsData', ['removeProduct', 'sortProdutcts'])
  }
}
</script>
<style scoped>
.products__header {
  display: flex;
  justify-content: flex-end;
  margin-bottom: 16px;
}
.product__cards {
  display: flex;
  grid-template-columns: auto;
  flex-wrap: wrap;
  justify-content: space-around;
}

@media (max-width: 720px) {
  .products__header {
    justify-content: center;
    margin: 16px 0;
  }
}
</style>
