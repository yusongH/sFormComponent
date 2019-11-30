<template>
  <div>
    <!-- 实现双向数据绑定 -->
    <!-- <s-input :value="modelData" @input="modelData = $event"></s-input>
    <input type="text" :value="modelData">-->

    <s-form :model="loginForm" :rules="rules" ref="loginForm">
      <s-form-item label="用户名" prop="userName">
        <s-input v-model="loginForm.userName"></s-input>
      </s-form-item>
      <s-form-item label="密码" prop="passWord">
        <s-input v-model="loginForm.passWord"></s-input>
      </s-form-item>
      <!-- <s-form-item label="邮箱" prop="passWord">
        <s-input v-model="loginForm.passWord"></s-input>
      </s-form-item>-->
      <s-form-item>
        <input type="button" value="登陆" @click="submitForm('loginForm')" />
      </s-form-item>
    </s-form>
  </div>
</template>

<script>
import sForm from "./sForm";
import sFormItem from "./sFormItem";
import sInput from "./sInput";
export default {
  components: {
    sForm,
    sFormItem,
    sInput
  },
  data() {
    return {
      loginForm: {
        userName: "",
        passWord: ""
      },
      modelData: "",
      rules: {
        userName: [
          { required: true, message: "请输入用户名", trigger: "blur" },
          { min: 3, max: 5, message: "长度在 3 到 5 个字符", trigger: "blur" }
        ],
        passWord: [{ required: true, message: "请输入密码", trigger: "blur" }]
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    }
  }
};
</script>

<style>
</style>