<template>
  <div>
    <h1>customer</h1>
    <div
      v-for="customer in customers"
      class="shadow-box flex gap-8 rounded-lg bg-white p-8"
    >
      <div class="w-[20%]">
        <h3 class="leading-4">
          <Icon name="tabler:id" color="black" class="mr-2 h-8 w-8" />Mã Tài Xế
        </h3>
        <h4 class="py-4">{{ customer._id }}</h4>
      </div>
      <div class="w-[10%]">
        <h3 class="leading-4">
          <Icon name="tabler:user" color="black" class="mr-2 h-8 w-8" />Mã Người
          Dùng
        </h3>
        <h4 class="py-4">{{ customer.userId }}</h4>
      </div>
      <div class="w-[10%]">
        <h3 class="leading-4">
          <Icon name="tabler:user" color="black" class="mr-2 h-8 w-8" />Họ và
          tên
        </h3>
        <h4 class="py-4">{{ customer.userId }}</h4>
      </div>
      <div class="w-[10%]">
        <h3 class="leading-4">
          <Icon name="tabler:mail" color="black" class="mr-2 h-8 w-8" />Email
        </h3>
        <h4 class="py-4">{{ customer.licenseNumber }}</h4>
      </div>
      <div class="w-[15%]">
        <h3 class="leading-4">
          <Icon name="tabler:phone" color="black" class="mr-2 h-8 w-8" />Số Điện
          Thoại
        </h3>
        <h4 class="py-4">{{ customer.state }}</h4>
      </div>
      <div class="w-[20%]">
        <h3 class="leading-4">
          <Icon
            name="tabler:calendar-time"
            color="black"
            class="mr-2 h-8 w-8"
          />Ngày Đăng Ký
        </h3>
        <h4 class="py-4">{{ customer.__v }}</h4>
      </div>
      <h1 class="flex border-0 text-center"></h1>
      <h1></h1>
      <button
        @click="deletecustomer(customer._id)"
        class="rounded-md bg-red-500 px-3 py-2 text-white hover:bg-red-600"
      >
        Delete
      </button>
    </div>
  </div>
</template>

<script lang="ts" setup>
const { data: customers } = useFetch(
  "https://findyourdriverapi-production.up.railway.app/customers/",
);

definePageMeta({
  layout: "dashboard-customer",
});
</script>

<style></style>
