<template>
  <div class="px-[15rem] py-[5vw]">
    <div v-if="pending">Loading...</div>
    <section v-if="customer">
      <h1>Thông tin cá nhân</h1>
      <form @submit.prevent="handleSubmit">
        <div class="my-4">
          <h3 class="py-2">Email</h3>
          <UInput type="email" v-model="customer.email" size="xl" />
        </div>
        <div class="my-4">
          <h3 class="py-2">Số Điện Thoại</h3>
          <UInput type="tel" v-model="customer.phone" size="xl" />
        </div>
        <UButton
          type="submit"
          color="black"
          variant="solid"
          class="ml-[auto] block"
          size="xl"
          >Cập Nhật</UButton
        >
      </form>
    </section>
    <div v-else-if="error">
      <h2>Đã có lỗi sảy ra</h2>
      <p>Không thể lấy thông tin khách hàng: {{ error.statusCode }}</p>
    </div>
  </div>
</template>

<script lang="ts" setup>
definePageMeta({
  layout: "dashboard-customer",
});
const id = useRoute().params.id;
const {
  data: customer,
  pending,
  error,
} = await useFetch("http://localhost:3001/users/" + id, {
  pick: ["email", "phone"],
});

const handleSubmit = async () => {
  const response = await useFetch("http://localhost:3001/users/" + id, {
    method: "PUT",
    body: customer,
  });
  alert(response.status._value);
  const res = response.status._value;
  if (res === "success") {
    console.log("Thông tin khách hàng đã được cập nhật");
  } else {
    console.error("Lỗi khi cập nhật thông tin khách hàng:", res);
  }
};

if (error.value) {
  console.error("Không thể lấy thông tin khách hàng:", error.value.message);
  console.error("Trạng Thái:", error.value.statusCode);
}
</script>
<style></style>
