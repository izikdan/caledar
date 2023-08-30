<script setup>
defineProps({
  email: String,
  tel: Number
})
</script>

<template>
  <div>
    <h4 class="green">{{ tel }} {{ email }}</h4>
    <a href="d0573193323@gmail.com">שלח לי מייל</a>
  </div>
</template>

<style>
/* .green {
  display: flex;
  justify-content: center;
  gap: 2px;
} */
</style>
