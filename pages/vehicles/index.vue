<template>
  <div>
    <h1>Vehicle</h1>
  </div>
</template>

<script lang="ts" setup>
const { data: vehicles } = useFetch(
  "https://findyourdriverapi-production.up.railway.app/vehicles/",
);
</script>

<style></style>
