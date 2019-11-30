<template>
  <div>
    <input :type="type" :value="value" @input="onInput" />
  </div>
</template>

<script>
export default {
  props: {
    type: {
      type: String,
      default: "text"
    },
    value: {
      type: String,
      default: ""
    }
  },
  methods: {
    onInput(e) {
      // 触发自身事件,将改变后的值传出去给父组件
      // ??weiheyidingweiinputshijian
      this.$emit("input", e.target.value);

      // 通知父组件进行校验
      this.$parent.$emit('validata')
    }
  }
};
</script>

<style>
</style>