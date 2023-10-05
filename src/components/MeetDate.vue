<script setup>
    import VueDatePicker from '@vuepic/vue-datepicker';
    import '@vuepic/vue-datepicker/dist/main.css'

defineProps({
  date: Date
})


</script>
<template>

      <h4> {{ date }}  </h4>     

</template>