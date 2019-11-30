<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  // 将自身组件让所有子组件都可访问
  provide() {
    return {
      form: this
    };
  },
  props: {
    model: {
      type: Object
    },
    rules: {
      type: Object
    }
  },
  methods: {
    async validate(callBack) {
      // 子组件校验为异步,因此返回promise
      var task = this.$children
        // 只有含有prop才需要校验
        .filter(item => item.prop)
        // 所有项进行校验
        .map(item => item.validata());
      var result = await Promise.all(task);
      if (result.some(valid => !valid)) {
        callBack(false);
      } else {
        callBack(true);
      }
    }
  }
};
</script>

<style>
</style>