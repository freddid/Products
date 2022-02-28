<template>
  <div class="product__filter" :class="{ show: showSelect }">
    <div @click="showSelect = !showSelect" class="select">
      {{ sortCondition }}
      <img src="@/assets/img/arrow.svg" alt="" />
    </div>
    <ul class="select__list">
      <li
        v-for="option in options"
        :key="option.val"
        class="select__option"
        :value="option.val"
        @click="selectOption(option)"
      >
        {{ option.txt }}
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data () {
    return {
      options: [
        { val: 'default', txt: 'По умолчанию' },
        { val: 'min', txt: 'По цене min' },
        { val: 'max', txt: 'По цене max' }
      ],
      sortCondition: 'По умолчанию',
      showSelect: false
    }
  },
  methods: {
    selectOption (option) {
      this.$emit('selectOption', option.val)
      this.sortCondition = option.txt
      this.showSelect = !this.showSelect
    }
  }
}
</script>
<style scoped>
.product__filter {
  font-size: 12px;
  color: #3f3f3f;
  position: relative;
}
.select {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  padding: 10px 16px;
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  min-width: 125px;
  line-height: 15px;
}
.select__list {
  width: calc(100% - 32px);
  background: #fffefb;
  padding: 10px 16px;
  position: absolute;
  list-style: none;
  margin: 0;
  z-index: 3;
  display: none;
  margin-top: 10px;
}
.select__option {
  text-align: center;
  cursor: pointer;
  padding: 7px 10px;
  margin: 4px 0;
  border-radius: 5px;
  background: rgb(221, 221, 221);
}

.select__option:hover {
  opacity: 0.7;
}

.select {
  cursor: pointer;
  display: flex;
  justify-content: space-between;
}
.show .select__list {
  display: block;
}
.show img {
  transform: rotate(180deg);
}
</style>
