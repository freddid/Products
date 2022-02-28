<template>
  <div class="add-product">
    <h1 class="add-product__title">Добавление товара</h1>
    <form class="add-product__form" action="#" @submit.prevent="validForm">
      <AddProductInput
        :val.sync="name"
        label="Наименование товара"
        placeholder="Введите наименование товара"
        :error="error.name"
      />

      <AddProductInput
        :val.sync="descript"
        :isTextarea="true"
        label="Описание товара"
        placeholder="Введите описание товара"
      />

      <AddProductInput
        :val.sync="urlImg"
        label="Ссылка на изображение товара"
        placeholder="Введите ссылку"
        :error="error.urlImg"
      />

      <AddProductInput
        :val.sync="price"
        label="Цена товара"
        type="number"
        placeholder="Введите цену"
        :error="error.price"
      />

      <button :class="{ disabled: emptiVal }" class="add-product__submit">
        Добавить товар
      </button>
    </form>
  </div>
</template>
<script>
import AddProductInput from '@/components/AddProduct/AddProductInput.vue'
import { mapGetters, mapMutations } from 'vuex'
export default {
  data () {
    return {
      name: '',
      descript: '',
      urlImg: '',
      price: '',
      error: {
        name: false,
        urlImg: false,
        price: false
      }
    }
  },
  components: {
    AddProductInput
  },
  methods: {
    validForm () {
      this.error.name = !this.name.length
      this.error.urlImg = !this.urlImg.length
      this.error.price = !this.price.length

      if (!this.emptiVal) {
        this.addProduct({
          id: Math.random(),
          name: this.name,
          urlImg: this.urlImg,
          price: +this.price,
          descript: this.descript
        })

        this.sortProdutcts(this.sortCondition)

        this.name = ''
        this.urlImg = ''
        this.price = ''
        this.descript = ''
      }
    },
    ...mapMutations('productsData', ['addProduct', 'sortProdutcts'])
  },
  computed: {
    emptiVal () {
      return !(this.name.length && this.urlImg.length && this.price.length)
    },
    ...mapGetters('productsData', ['sortCondition'])
  }
}
</script>
<style scoped>
.add-product__form {
  background: #fffefb;
  padding: 24px;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
}

.add-product__title {
  margin-bottom: 16px;
  font-size: 28px;
  color: #3f3f3f;
  line-height: 35px;
}

.add-product__submit.disabled {
  background: #eeeeee;
  box-shadow: none;
  color: #b4b4b4;
}
.add-product__submit {
  background: #7bae73;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  color: #ffffff;
  padding: 10px 0;
  cursor: pointer;
  width: 100%;
  border-radius: 10px;
  font-weight: 600;
  line-height: 15px;
  font-size: 12px;
}
</style>
