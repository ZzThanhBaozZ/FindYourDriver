<template>
  <div class="flex justify-center p-[150px]">
    <section
      class="justify-left flex w-[50vw] flex-col items-center rounded-lg border border-gray-400 bg-gray-100 bg-white p-[40px]"
    >
      <div class="py-[40px]">
        <h1>Đăng nhập tài khoản của bạn</h1>
        <h3>Điền thông tin của bạn ở dưới đây</h3>
      </div>
      <div class="w-1/2">
        <form
          action=""
          class="flex w-[100%] flex-col gap-[20px]"
          @submit.prevent="login"
        >
          <UFormGroup label="Email hoặc Số Điện Thoại">
            <UInput
              placeholder="you@example.com"
              icon="i-heroicons-envelope"
              v-model="phoneEmail"
            />
          </UFormGroup>
          <UFormGroup label="Mật khẩu">
            <UInput
              placeholder="Mật Khẩu"
              icon="i-heroicons-envelope"
              v-model="password"
            />
          </UFormGroup>
          <div class="flex justify-between py-[20px]">
            <UButton label="Đăng Nhập" type="submit" />
            <NuxtLink to="/register">Bạn Chưa Đăng Ký?</NuxtLink>
          </div>
        </form>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue"; // Import ref for reactivity

const phoneEmail = ref("");
const password = ref("");

async function login() {
  const bodyToSend = {
    phoneEmail: phoneEmail.value,
    password: password.value,
  };
  console.log("body to send:", bodyToSend); // Inspect before sending
  try {
    const response = await $fetch(
      "https://findyourdriverapi-production.up.railway.app/login/",
      {
        method: "POST",
        body: bodyToSend,
      },
    );
    // console.log("respond:", response);
    // console.log("Trạng thái phản hồi:", response.status);
    const Userid = response.userId;
    const isDriver = response.isDriver;
    console.log("Id của người dùng này:", response.userId);
    console.log("Có phải là tài xế không:", isDriver);
    if (isDriver === false) {
      const toast = useToast();
      toast.add({
        id: "update_downloaded",
        title: "Đăng nhập thành công",
        description: "Bạn sẽ được chuyển sang trang cá nhân của bạn",
        icon: "i-heroicons-light-bulb",
        timeout: 1500,
      });
      await new Promise((resolve) => setTimeout(resolve, 1500));
      await navigateTo({ path: `/customers/${Userid}` });
    }

    // if (response.ok) {
    //   const data = await response.json(); // Parse JSON response
    //   if (data.success) {
    //     const userId = data.user._id;
    //     console.log("User ID:", userId);
    //   } else {
    //     console.error("Login failed:", data);
    //   }
    // } else {
    //   // Some other error aside from incorrect credentials occurred
    //   console.error("Login failed:", response);
    // }
  } catch (error) {
    console.error("Login error:", error);
  }
}
//////////////////////////Notification
const toast = useToast();

onMounted(() => {
  toast.add({
    id: "update_downloaded",
    title: "Đây là phần đăng nhập tài khoản",
    description: "Bạn hãy nhập thông tin cần thiết vào mẫu sau",
    icon: "i-heroicons-light-bulb",
    timeout: 3000,
  });
});
</script>

<style>
* {
  outline: 1px solid rgba(255, 0, 0, 0.01);
}
</style>
