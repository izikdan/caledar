<script setup>
defineProps({
  email: String,
  tel: Number
})
</script>

<template>
  <div>
    <h5 class="green">{{ tel }} {{ email }} שלח מייל</h5>
    <!-- <a href="mailto:d0573193323@gmail.com">שלח לי מייל</a> -->
    <!-- <a https="//wa.me/+972533193323">שלח ווצאפ</a> -->
  </div>
</template>

<style>
/* .green {
  display: flex;
  justify-content: center;
  gap: 2px;
} */
</style>
