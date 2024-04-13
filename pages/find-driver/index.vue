<template>
  <div>
    <form @submit.prevent="findDriver(formData)" class="w-1/4">
      <UFormGroup label="Kinh Độ">
        <UInput placeholder="Nguyễn Văn A" icon="i-heroicons-user-16-solid" />
      </UFormGroup>
      <UFormGroup label="Vĩ Độ">
        <UInput placeholder="you@example.com" icon="i-heroicons-envelope" />
      </UFormGroup>
      <button type="submit" class="my-4 rounded-full bg-[#24a0ed] p-2">
        Thêm Người dùng
      </button>
    </form>
  </div>
</template>

<script lang="ts" setup>
const { data: drivers } = useFetch("http://localhost:3001/find-driver/");
async function findDriver(findDriver) {
  try {
    const response = await fetch(`http://localhost:3001/drivers/`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(findDriver),
    });

    if (response.ok) {
      // Add the newly created user to the drivers array (optimistic update)
      const createdUser = await response.json();
      drivers.value.unshift(createdUser);
    } else {
      console.error("Create failed:", response.status);
      // Handle the error appropriately
    }
  } catch (error) {
    console.error("Error during create:", error);
    // Handle the error
  }
}
</script>

<style></style>
