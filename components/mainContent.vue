<template>
  <main class="default-px relative left-[20vw] flex w-[80vw] flex-col border">
    <section class="flex flex-col gap-4">
      <div>
        <div class="shadow-box inline-block rounded-lg bg-white p-8">
          <h1 class="leading-[4rem]">QUẢN LÝ NGƯỜI DÙNG</h1>
          <div class="space-x-2">
            <UBadge size="lg" color="blue">GET</UBadge>
            <UBadge size="lg">POST</UBadge>
            <UBadge size="lg" color="orange">PUT</UBadge>
            <UBadge size="lg" color="red">DELETE</UBadge>
          </div>
        </div>
      </div>
      <form @submit.prevent="postUser" class="w-1/4">
        <UFormGroup label="Họ và Tên">
          <UInput
            placeholder="Nguyễn Văn A"
            icon="i-heroicons-user-16-solid"
            v-model="fullName"
          />
        </UFormGroup>
        <UFormGroup label="Email">
          <UInput
            placeholder="you@example.com"
            icon="i-heroicons-envelope"
            v-model="email"
          />
        </UFormGroup>
        <UFormGroup label="Số Điện Thoại">
          <UInput
            placeholder="0919999999"
            icon="i-heroicons-phone"
            v-model="phone"
          />
        </UFormGroup>
        <UFormGroup label="Mat khau">
          <UInput
            placeholder="2512512612376"
            icon="i-heroicons-phone"
            v-model="password"
          />
        </UFormGroup>
        <button
          type="submit"
          class="my-4 rounded-full bg-[#24a0ed] p-2"
          :disabled="refreshing"
          @click="refreshAll"
        >
          Thêm Người dùng
        </button>
      </form>
      <div
        v-for="user in users"
        class="shadow-box flex gap-8 rounded-lg bg-white p-8"
      >
        <div class="w-[20%]">
          <h3 class="leading-4">
            <Icon name="tabler:id" color="black" class="mr-2 h-8 w-8" />Mã người
            dùng
          </h3>
          <h4 class="py-4">{{ user._id }}</h4>
        </div>
        <div class="w-[20%]">
          <h3 class="leading-4">
            <Icon name="tabler:user" color="black" class="mr-2 h-8 w-8" />Họ và
            tên
          </h3>
          <h4 class="py-4">{{ user.fullName }}</h4>
        </div>
        <div class="w-[10%]">
          <h3 class="leading-4">
            <Icon name="tabler:mail" color="black" class="mr-2 h-8 w-8" />Email
          </h3>
          <h4 class="py-4">{{ user.email }}</h4>
        </div>
        <div class="w-[15%]">
          <h3 class="leading-4">
            <Icon name="tabler:phone" color="black" class="mr-2 h-8 w-8" />Số
            Điện Thoại
          </h3>
          <h4 class="py-4">{{ user.phone }}</h4>
        </div>
        <div class="w-[20%]">
          <h3 class="leading-4">
            <Icon
              name="tabler:calendar-time"
              color="black"
              class="mr-2 h-8 w-8"
            />Ngày Đăng Ký
          </h3>
          <h4 class="py-4">{{ user.registrationDate }}</h4>
        </div>
        <h1 class="flex border-0 text-center"></h1>
        <h1></h1>
        <button
          @click="deleteUser(user._id)"
          class="rounded-md bg-red-500 px-3 py-2 text-white hover:bg-red-600"
        >
          Delete
        </button>
      </div>
    </section>
  </main>
</template>

<script lang="ts" setup>
const { data: users } = useFetch(
  "https://findyourdriverapi-production.up.railway.app/users",
);

async function deleteUser(userId) {
  try {
    const response = await fetch(
      `https://findyourdriverapi-production.up.railway.app/users/${userId}`,
      {
        method: "DELETE",
        headers: {
          "Content-Type": "application/json",
        },
      },
    );

    if (response.ok) {
      users.value = users.value.filter((user) => user._id !== userId);
      console.log("User deleted successfully");
    } else {
      throw new Error("Error deleting user");
    }
  } catch (error) {
    console.error(error);
  }
}

import { ref } from "vue"; // Import ref for reactivity

const fullName = ref("");
const email = ref("");
const phone = ref("");
const password = ref("");

async function postUser() {
  const bodyToSend = {
    fullName: fullName.value,
    email: email.value,
    phone: phone.value,
    password: password.value,
  };
  console.log("body to send:", bodyToSend); // Inspect before sending
  try {
    const response = await $fetch(
      "https://findyourdriverapi-production.up.railway.app/users/",
      {
        method: "POST",
        body: bodyToSend,
      },
    );
    console.log("respond:", response);
    if (response === "User added!") {
      console.log("Thêm thành công");
      const toast = useToast();
      toast.add({
        id: "update_downloaded",
        title: "Thêm người dùng thành công",
        description: "Dữ liệu sẽ được cập nhật lại sau chốc lát",
        icon: "i-heroicons-light-bulb",
        timeout: 1500,
      });
    }
  } catch (error) {
    console.error("Login error:", error);
  }
}
/////////////////////Reload
const refreshing = ref(false);
const refreshAll = async () => {
  await new Promise((resolve) => setTimeout(resolve, 4000));
  refreshing.value = true;
  try {
    await refreshNuxtData();
  } finally {
    refreshing.value = false;
  }
};
</script>

<style></style>
