<template>
  <div class="add-product">
    <h1 class="add-product__title">Добавление товара</h1>
    <form class="add-product__form" action="#" @submit.prevent="validForm">
      <AddProductInput
        v-for="input in inputObj"
        :key="input.label"
        :val.sync="input.val"
        :label="input.label"
        :type="input.type"
        :isTextarea="input.isTextarea"
        :placeholder="input.placeholder"
        :required="input.required"
        :error="input.error"
      />
      <button :class="{ disabled: emptiVal }" class="add-product__submit">
        Добавить товар
      </button>
      <div v-if="success" class="success">Товар успешно добавлен</div>
    </form>
  </div>
</template>
<script>
import AddProductInput from '@/components/AddProduct/AddProductInput.vue'
import { mapGetters, mapMutations } from 'vuex'
export default {
  data () {
    return {
      inputObj: [
        {
          val: '',
          name: 'name',
          label: 'Наименование товара',
          placeholder: 'Введите наименование товара',
          error: false,
          required: true
        },
        {
          val: '',
          name: 'descript',
          isTextarea: true,
          label: 'Описание товара',
          placeholder: 'Введите описание товара',
          required: false,
          error: false
        },
        {
          val: '',
          name: 'urlImg',
          label: 'Ссылка на изображение товара',
          placeholder: 'Введите ссылку',
          error: false,
          required: true
        },
        {
          val: '',
          name: 'price',
          label: 'Цена товара',
          placeholder: 'Введите цену',
          type: 'number',
          error: false,
          required: true
        }
      ],
      success: false
    }
  },
  components: {
    AddProductInput
  },
  methods: {
    validForm () {
      this.inputObj.forEach(el => (el.error = !el.val.length))

      if (!this.emptiVal) {
        this.addProduct({
          id: Math.random() + this.inputObj[0].val,
          name: this.inputObj[0].val,
          descript: this.inputObj[1].val,
          urlImg: this.inputObj[2].val,
          price: this.inputObj[3].val
        })
        this.sortProdutcts(this.sortCondition)
        this.inputObj.forEach(el => (el.val = ''))

        this.success = true
        setTimeout(() => (this.success = false), 2000)
      }
    },
    ...mapMutations('productsData', ['addProduct', 'sortProdutcts'])
  },
  computed: {
    emptiVal () {
      return this.inputObj.find(el => el.val == '' && el.required)
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

.success {
  text-align: center;
  margin-top: 16px;
  display: block;
  border-radius: 10px;
  font-weight: 600;
  color: #7bae73;
  font-size: 16px;
}
</style>
