<template>
  <div class="flex">
    <section class="w-1/2">
      <form @submit.prevent="findDrivers" class="w-1/4">
        <UFormGroup label="Vĩ Độ">
          <UInput placeholder="100" v-model="pickupLat" />
        </UFormGroup>
        <UFormGroup label="Kinh Độ">
          <UInput placeholder="100" v-model="pickupLng" />
        </UFormGroup>
        <div class="w-1/2">
          <USelect
            v-model="vehicleType"
            :options="vehicleTypes"
            option-attribute="name"
            size="2xs"
          />
        </div>
        <button type="submit" class="my-4 rounded-full bg-[#24a0ed] p-2">
          Tìm kiếm tài xế
        </button>
      </form>
    </section>
    <section v-if="driverData">
      <ul>
        <li>Họ và Tên: {{ driverData.fullName }}</li>
        <li>Biển số xe: {{ driverData.licenseNumber }}</li>
        <li>Đánh giá: {{ driverData.rating }}/5</li>
        <li>Trạng Thái: {{ driverData.available }}</li>
      </ul>
      <div
        style="
          max-width: 100%;
          list-style: none;
          transition: none;
          overflow: hidden;
          width: 100%;
          height: 500px;
        "
      >
        <div
          id="my-map-canvas"
          style="height: 100%; width: 100%; max-width: 100%"
        >
          <iframe
            :src="
              'https://www.google.com/maps/embed/v1/place?q=' +
              driverData.latitude +
              ',' +
              driverData.longitude +
              '&key=AIzaSyBFw0Qbyq9zTFTd-tUY6dZWTgaQzuU17R8'
            "
            width="100%"
            height="450"
          ></iframe>
        </div>
      </div>
    </section>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue"; // Import ref for reactivity
definePageMeta({
  layout: "dashboard-customer",
});

const { data: vehicleTypes } = useFetch(
  "https://findyourdriverapi-production.up.railway.app/vehicle-type/",
);
const vehicleType = ref(null);

const pickupLat = ref("");
const pickupLng = ref("");
const driverData = ref(null);
async function findDrivers() {
  const bodyToSend = {
    pickupLat: pickupLat.value,
    pickupLng: pickupLng.value,
    vehicleType: vehicleType.value,
  };
  console.log("Selected vehicleType:", vehicleType.value);
  console.log("body to send:", bodyToSend); // Inspect before sending
  try {
    const response = await $fetch(
      "https://findyourdriverapi-production.up.railway.app/find-driver/",
      {
        method: "POST",
        body: bodyToSend,
      },
    );
    console.log(response);
    driverData.value = response;
  } catch (error) {
    console.error("Login error:", error);
  }
}
</script>

<style></style>
