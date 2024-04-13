<template>
  <div>
    <h1>Vehicle</h1>
  </div>
</template>

<script lang="ts" setup>
const { data: vehicles } = useFetch("http://localhost:3001/vehicles/");
</script>

<style></style>
