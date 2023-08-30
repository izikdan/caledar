<script setup>
defineProps({
  name: String,
  date: Date
})

// const name = ref("")
// const date = ref("")
</script>
<template>

      <h2>{{ name }} - {{ date }}  </h2>
</template>