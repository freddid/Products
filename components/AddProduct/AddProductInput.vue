<template>
  <div class="form-group">
    <label for="add-product__input">
      {{ label }} <i v-if="!isTextarea"></i>
    </label>
    <input
      :class="{ error: error }"
      v-if="!isTextarea"
      @input="change"
      :value="val"
      :type="type"
      id="add-product__input"
      :placeholder="placeholder"
    />
    <textarea
      v-else
      @input="change"
      :value="val"
      :type="type"
      id="add-product__input"
      :placeholder="placeholder"
    />
    <small class="add-product__error" v-if="error"
      >Поле является обязательным</small
    >
  </div>
</template>
<script>
export default {
  props: {
    placeholder: {
      type: String,
      default: ''
    },
    isTextarea: {
      type: Boolean,
      default: false
    },
    error: {
      type: Boolean,
      default: false
    },
    type: {
      type: String,
      default: 'text'
    },
    label: {
      type: String,
      default: ''
    },
    val: {
      type: String,
      default: ''
    }
  },
  emits: ['update:val'],
  methods: {
    change (e) {
      this.$emit('update:val', e.target.value)
    }
  }
}
</script>
<style scoped>
.form-group {
  margin-bottom: 16px;
  display: flex;
  position: relative;
  flex-wrap: wrap;
}
#add-product__input {
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  font-size: 12px;
  padding: 10px 16px;
  width: 100%;
}
label[for='add-product__input'] {
  font-size: 10px;
  color: #49485e;
  margin-bottom: 5px;
  position: relative;
  width: max-content;
}
label[for='add-product__input'] i::before {
  background: #ff8484;
  content: '';
  right: -7px;
  width: 4px;
  position: absolute;
  height: 4px;
  border-radius: 4px;
}
textarea#add-product__input {
  resize: none;
  height: 108px;
}
.add-product__error {
  font-size: 8px;
  position: absolute;
  bottom: -13px;
  line-height: 10px;
  color: #ff8484;
}

#add-product__input.error {
  border: 1px solid #ff8484;
}
</style>
