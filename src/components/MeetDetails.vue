<script setup>

defineProps({
  details: String,
  
})

// const name = ref("")
// const date = ref("")
</script>
<template>
      <h4 class="green">  {{ details }}  </h4>
      <!-- <div class="actions">
            <button @click="deleteMeet(index)">מחק</button>
            <button @click="editMeet(index)">ערוך</button> 
            <button @click="saveEdit">שמור עריכה</button>
                  <label for="pay"> <input id="pay" type="checkbox">שילם</label>
          </div> -->
</template> 
<!-- <style> -->
/* .green{
 display: flex;
  gap: 100px;
  justify-content: center;
  /* background-color: rgb(0, 255, 208); */
/* }
  
<!-- </style> -->