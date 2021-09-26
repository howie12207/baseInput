<script setup>
import { ref } from "vue";
import BaseInput from "/src/components/BaseInput.vue";

const account = ref({
  inputValue: "",
  isValid: false,
  rules: {
    isRequired: true,
    min: 4,
    max: 12,
    limit: "enAndNumber",
  },
});
const password = ref({
  inputValue: "",
  isValid: false,
  rules: {
    isRequired: true,
    min: 4,
    max: 12,
    limit: "enAndNumber",
  },
});
const confirmPassword = ref({
  inputValue: "",
  isValid: false,
  rules: {
    isRequired: true,
    min: 4,
    max: 12,
    limit: "enAndNumber",
  },
  errMsg: "",
});

const confirmPwd = (target) => {
  if (target === "first" && confirmPassword.value.inputValue === "") return;
  if (password.value.inputValue !== confirmPassword.value.inputValue) {
    if (target === "first") confirmPassword.value.isValid = false;
    confirmPassword.value.errMsg = "密碼不同";
  } else {
    if (target === "first") confirmPassword.value.isValid = true;
    confirmPassword.value.errMsg = "";
  }
};
</script>

<template>
  <div>
    <BaseInput
      v-model:inputValue="account.inputValue"
      v-model:isValid="account.isValid"
      label="請輸入帳號"
      id="account"
      :rules="account.rules"
    />
    <BaseInput
      v-model:inputValue="password.inputValue"
      v-model:isValid="password.isValid"
      label="請輸入密碼"
      id="password"
      type="text"
      :rules="password.rules"
      @onBlur="confirmPwd('first')"
      @onKeyup="confirmPwd('first')"
    />
    <BaseInput
      v-model:inputValue="confirmPassword.inputValue"
      v-model:isValid="confirmPassword.isValid"
      label="請輸入確認密碼"
      id="confirmPassword"
      type="text"
      :rules="confirmPassword.rules"
      :errMsg="confirmPassword.errMsg"
      @onBlur="confirmPwd"
      @onKeyup="confirmPwd"
    />
  </div>
</template>

<style scoped></style>
