<template>
  <main
    class="default-px relative left-[20vw] flex h-[200vh] w-[80vw] flex-col border"
  >
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
      <form @submit.prevent="createUser(formData)" class="w-1/4">
        <UFormGroup label="Họ và Tên">
          <UInput placeholder="Nguyễn Văn A" icon="i-heroicons-user-16-solid" />
        </UFormGroup>
        <UFormGroup label="Email">
          <UInput placeholder="you@example.com" icon="i-heroicons-envelope" />
        </UFormGroup>
        <UFormGroup label="Số Điện Thoại">
          <UInput placeholder="0919999999" icon="i-heroicons-phone" />
        </UFormGroup>
        <UFormGroup label="Mat khau">
          <UInput placeholder="2512512612376" icon="i-heroicons-phone" />
        </UFormGroup>
        <button type="submit" class="my-4 rounded-full bg-[#24a0ed] p-2">
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
        <div class="w-[10%]">
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
      <div>
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d10535.508890495077!2d105.84282512604092!3d20.99805238919978!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3135ac73d357ec99%3A0xc31f64fdce94db24!2zS8OtIHTDumMgeMOhIMSQ4bqhaSBo4buNYyBLaW5oIHThur8gUXXhu5FjIETDom4!5e0!3m2!1svi!2s!4v1712667104433!5m2!1svi!2s"
          width="100%"
          height="450"
          style="border: 0"
          allowfullscreen="true"
          loading="lazy"
          referrerpolicy="no-referrer-when-downgrade"
        ></iframe>
        <div class="relative z-[999]">
          <Icon
            name="tabler:phone"
            color="black"
            class="fixed left-1/2 top-1/2 z-[999] -translate-x-1/2 -translate-y-1/2 transform"
          >
            Tài xế
          </Icon>
        </div>
      </div>
    </section>
  </main>
</template>

<script lang="ts" setup>
const { data: users } = useFetch("http://localhost:3001/users");

async function deleteUser(userId) {
  try {
    const response = await fetch(`http://localhost:3001/users/${userId}`, {
      method: "DELETE",
      headers: {
        "Content-Type": "application/json",
      },
    });

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

async function createUser(newUserData) {
  try {
    const response = await fetch(`http://localhost:3001/users/`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(newUserData),
    });

    if (response.ok) {
      const createdUser = await response.json();
      users.value.unshift(createdUser);
    } else {
      console.error("Create failed:", response.status);
    }
  } catch (error) {
    console.error("Error during create:", error);
  }
}
</script>

<style></style>
