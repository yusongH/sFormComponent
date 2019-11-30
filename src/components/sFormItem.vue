<template>
  <div>
    <span v-if="label">{{label}}</span>
    <slot></slot>
    <div v-if="errorMessage">{{errorMessage}}</div>
  </div>
</template>

<script>
import Validator from "async-validator";
export default {
  // 注入父组件
  inject: ["form"],
  data() {
    return {
      errorMessage: ""
    };
  },
  props: {
    label: {
      type: String,
      default: ""
    },
    prop: {
      type: String,
      default: ""
    }
  },
  created() {
    // 监听子组件检验通知
    this.$on("validata", this.validata);
  },
  methods: {
    validata() {
      return new Promise(resolve => {
        // 指定校验规则
        var descriptor = { [this.prop]: this.form.rules[this.prop] };
        var validator = new Validator(descriptor);
        validator.validate(
          { [this.prop]: this.form.model[this.prop] },
          errors => {
            if (errors) {
              this.errorMessage = errors[0].message;
              resolve(false);
            } else {
              this.errorMessage = "";
              resolve(true);
            }
          }
        );
      });
    }
  }
};
</script>

<style>
</style>