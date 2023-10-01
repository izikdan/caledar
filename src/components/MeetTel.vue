<script setup>
defineProps({
  tel: Number
})
</script>

<template>
  <div>
    <h5 class="green">{{ tel }} <button>שלח ווצאפ</button> </h5>
  </div>
</template>

<style>
/* .green {
  display: flex;
  justify-content: center;
  gap: 2px;
} */
</style>
