<script setup>
defineProps({
  email: String
})
</script>

<template>
  <div>
    <h5 class="green"> {{ email }} <button>שלח מייל</button> </h5>
  </div>
</template>

<style>
/* .green {
  display: flex;
  justify-content: center;
  gap: 2px;
} */
</style>
