<template>
  <div class="fixed top-0 h-[100vh] w-[20vw] bg-gray-200 p-2">
    <div class="flex h-full flex-col justify-between">
      <section>
        <NuxtImg src="/Superspeed.svg" class="m-auto block w-[10vw] pr-[2vw]" />
        <div class="flex flex-col items-center justify-center gap-4 py-10">
          <NuxtLink to="/drivers">
            <UButton size="xl">Quản Lý Tài Xế</UButton>
          </NuxtLink>
          <NuxtLink to="/find-driver">
            <UButton size="xl">Tìm Tài Xế</UButton>
          </NuxtLink>
          <NuxtLink to="/vehicle-types">
            <UButton size="xl">Loại Phương Tiện</UButton>
          </NuxtLink>
          <NuxtLink to="/vehicles">
            <UButton size="xl">Thống Kê Xe</UButton>
          </NuxtLink>
        </div>
      </section>
      <section class="flex justify-center py-4">
        <NuxtLink to="/">
          <UButton color="red" size="xl">Đăng Xuất</UButton>
        </NuxtLink>
      </section>
    </div>
  </div>
</template>

<script lang="ts" setup></script>

<style></style>
