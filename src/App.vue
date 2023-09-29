<script setup>
import ToDo from "@components/ToDo.vue"

</script>

<template>
  <div class="app w3-blue-gray">
    <ToDo/>
  </div>
</template>

<style scoped>
.app{
  display: flex;
  place-content: center;
  width: 100vw;
  min-height: 100vh;
  padding: 5rem;
}
</style>
