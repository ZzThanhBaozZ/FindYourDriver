<template>
  <div class="flex justify-center p-[150px]">
    <section
      class="justify-left flex w-[50vw] flex-col items-center rounded-lg border border-gray-400 bg-gray-100 bg-white p-[40px]"
    >
      <div class="py-[40px]">
        <h1>Đăng ký tài khoản của bạn</h1>
        <h3>Điền thông tin của bạn ở dưới đây</h3>
      </div>
      <div class="w-1/2">
        <form action="" class="flex w-[100%] flex-col gap-[20px]">
          <UFormGroup label="Họ và tên*">
            <UInput
              v-model="formData.fullName"
              placeholder="Tran Thanh Dat"
              type="text"
              icon="i-heroicons-envelope"
              required
            />
          </UFormGroup>
          <UFormGroup label="Email*">
            <UInput
              v-model="formData.email"
              placeholder="you@example.com"
              type="email"
              icon="i-heroicons-envelope"
              required
            />
          </UFormGroup>
          <UFormGroup label="Số Điện Thoại *">
            <UInput
              v-model="formData.phone"
              placeholder="091*******"
              type="tel"
              icon="i-heroicons-envelope"
              required
            />
          </UFormGroup>
          <UFormGroup label="Mật khẩu *">
            <UInput
              v-model="formData.password"
              placeholder="Mật Khẩu"
              type="password"
              icon="i-heroicons-envelope"
              required
            />
          </UFormGroup>
          <button type="submit" :disabled="loading">
            {{ loading ? "Registering..." : "Register" }}
          </button>
          <div v-if="error" class="error-message">{{ error }}</div>
          <div v-if="success" class="success-message">
            Registration Successful!
          </div>
        </form>
        <URadioGroup v-model="selected" legend="Bạn là:" :options="options" />
        <div class="flex justify-between py-[20px]">
          <UButton label="Đăng Ký" />
          <NuxtLink to="/login">Bạn Đã Có Tài Khoản?</NuxtLink>
        </div>
      </div>
    </section>
  </div>
</template>
<script lang="ts" setup>
const options = [
  {
    value: "0",
    label: "Khách Hàng",
  },
  {
    value: "1",
    label: "Tài Xế",
  },
];

const selected = ref("sms");

import { ref } from "vue";

const formData = ref({
  fullName: "",
  email: "",
  phone: "",
  password: "",
});

const loading = ref(false);
const error = ref(null);
const success = ref(false); // Track success

async function registerUser() {
  loading.value = true;
  error.value = null;
  success.value = false; // Reset success

  try {
    const response = await fetch(
      "https://findyourdriverapi-production.up.railway.app/register",
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(formData.value),
      },
    );

    if (!response.ok) {
      throw new Error(`API request failed with status ${response.status}`);
    }

    const data = await response.json();
    console.log("Registration successful:", data);
    success.value = true; // Registration success!
  } catch (err) {
    error.value = err.message;
  } finally {
    loading.value = false;
  }
}
</script>

<style>
* {
  outline: 1px solid rgba(255, 0, 0, 0.01);
}
.error-message {
  color: red;
  font-weight: bold;
}
.success-message {
  color: green;
  font-weight: bold;
}
</style>
