<template>
  <div>
    <h1>Driver</h1>
    <div
      v-for="driver in drivers"
      :key="driver._id"
      class="shadow-box flex flex-col gap-8 rounded-lg bg-white p-8"
    >
      <div class="flex">
        <div class="flex w-full">
          <div class="w-[15vw]">
            <h3 class="leading-4">
              <Icon
                name="tabler:id"
                color="black"
                class="mr-2 h-8 w-8 pb-1"
              />Mã Tài Xế
            </h3>
            <h4 class="py-4">{{ driver._id }}</h4>
          </div>
          <div class="w-[10vw]">
            <h3 class="leading-4">
              <Icon
                name="tabler:user"
                color="black"
                class="mr-2 h-8 w-8 pb-1"
              />Biển Số Xe
            </h3>
            <h4 class="py-4">{{ driver.fullName }}</h4>
          </div>
          <div class="w-[15vw]">
            <h3 class="leading-4">
              <Icon
                name="solar:plate-broken"
                color="black"
                class="mr-2 h-8 w-8 pb-1"
              />Biển Số Xe
            </h3>
            <h4 class="py-4">{{ driver.licenseNumber }}</h4>
          </div>
          <div class="w-[10vw]">
            <h3 class="leading-4">
              <Icon
                name="flowbite:star-outline"
                color="black"
                class="mr-2 h-8 w-8 pb-1"
              />Đánh giá
            </h3>
            <h4 class="py-4">{{ driver.rating }}/5</h4>
          </div>
          <div class="w-[15vw]">
            <h3 class="leading-4">
              <Icon
                name="tabler:world-latitude"
                color="black"
                class="mr-2 h-8 w-8 pb-1"
              />Vĩ Độ
            </h3>
            <h4 class="py-4">{{ driver.latitude }}</h4>
          </div>
          <div class="w-[15vw]">
            <h3 class="leading-4">
              <Icon
                name="tabler:world-longitude"
                color="black"
                class="mr-2 h-8 w-8 pb-1"
              />Kinh Độ
            </h3>
            <h4 class="py-4">{{ driver.longitude }}</h4>
          </div>
          <div class="w-[10vw]">
            <h3 class="leading-4">
              <Icon
                name="fluent:presence-available-10-regular"
                color="black"
                class="mr-2 h-8 w-8 pb-1"
              />
              Tình Trạng
            </h3>
            <h4 class="py-4">
              <span v-if="driver.available === true">Sẵn sàng</span>
              <span v-if="driver.available !== true">Bận</span>
            </h4>
          </div>
        </div>
        <div>
          <button
            @click="deleteDriver(driver._id)"
            class="rounded-md bg-red-500 px-4 py-2 text-white hover:bg-red-600"
          >
            Xóa Tài Xế
          </button>
        </div>
      </div>
      <section>
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
                driver.latitude +
                ',' +
                driver.longitude +
                '&key=AIzaSyBFw0Qbyq9zTFTd-tUY6dZWTgaQzuU17R8'
              "
              width="100%"
              height="450"
            ></iframe>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script lang="ts" setup>
//GET METHOD
const { data: drivers } = useFetch(
  "https://findyourdriverapi-production.up.railway.app/drivers/",
);

//DELETE METHOD
async function deleteDriver(DriverId) {
  try {
    const response = await fetch(
      `https://findyourdriverapi-production.up.railway.app/drivers/${DriverId}`,
      {
        method: "DELETE",
        headers: {
          "Content-Type": "application/json",
        },
      },
    );

    if (response.ok) {
      drivers.value = drivers.value.filter((driver) => driver._id !== DriverId);
      console.log("driver deleted successfully");
    } else {
      throw new Error("Error deleting driver");
    }
  } catch (error) {
    console.error(error);
  }
}
</script>

<style></style>
