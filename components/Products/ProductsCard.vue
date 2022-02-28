<template>
  <div class="product__card">
    <div class="product__img">
      <img :src="src" alt="Здесь должно было быть изображение" />
    </div>
    <div class="product__card__contant">
      <div class="product__card__title">{{ title }}</div>
      <div class="product__card__txt">{{ txt }}</div>
      <div class="product__card__price">{{ price }}</div>
    </div>
    <div @click="$emit('removeProduct', id)" class="product__card__basket">
      <img src="@/assets/img/basket-icon.svg" alt="" />
    </div>
  </div>
</template>
<script>
export default {
  props: {
    src: {
      type: String,
      default: ''
    },
    title: {
      type: String,
      default: ''
    },
    txt: {
      type: String,
      default: ''
    },
    price: {
      type: Number,
      default: 0
    },
    id: {
      type: Number,
      default: null
    }
  }
}
</script>
<style scoped>
.product__card {
  position: relative;
  width: 332px;
  color: #3f3f3f;
  cursor: pointer;
  background: #fffefb;
  margin-bottom: 16px;
  box-shadow: 0px 20px 30px rgb(0 0 0 / 4%), 0px 6px 10px rgb(0 0 0 / 2%);
  margin-left: 16px;
  border-radius: 4px;
  transition: all 0.3s;
}
.product__card__contant {
  padding: 16px;
}
.product__img img {
  width: 100%;
  height: 100%;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
}
.product__card__txt {
  margin: 16px 0 32px 0;
  font-size: 16px;
  line-height: 20px;
}
.product__img {
  height: 200px;
  display: flex;
}
.product__card__title {
  font-weight: 600;
  font-size: 20px;
  line-height: 25px;
}
.product__card__price {
  font-weight: 600;
  font-size: 24px;
  line-height: 30px;
}
.product__card__basket {
  position: absolute;
  background: #ff8484;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  display: none;
  justify-content: center;
  align-items: center;
  top: -10px;
  right: -10px;
  width: 32px;
  height: 32px;
}
.product__card:hover .product__card__basket {
  display: flex;
}
.product__card:hover {
  box-shadow: 0px 0px 20px 6px rgb(0 0 0 / 17%);
}
.product__card__basket:hover {
  background: #ff5151;
}
</style>
