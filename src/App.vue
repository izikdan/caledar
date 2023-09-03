<script setup>
import MeetInfo from './components/MeetInfo.vue'
import MeetDetails from './components/MeetDetails.vue'
import MeetEmail from './components/MeetEmail.vue'
import PlaceSudy from './components/PlaceStudy.vue'
import { ref , onMounted } from 'vue'
import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css';
// import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
// import { faEnvelope } from '@fortawesome/free-solid-svg-icons';


let meets = ref([]);
let meet = ref({});
let selectedMeet = ref(null);
let myCanvas = ref(null);

const meetLocal = JSON.parse(localStorage.getItem("meets"));
if (meetLocal) {
  meets.value = meetLocal;
}
onMounted(() => {
  const canvas = myCanvas.value;
  const ctx = canvas.getContext('2d');
  if (ctx) {
  ctx.moveTo(0,0);
ctx.lineTo(200,100);
ctx.stroke();
  }
  } );
const addMeet = (e) => {
  let newMeet = { ...meet.value }
  meets.value.push(newMeet)
  meet.value.name = '';
  meet.value.date = '';
  meet.value.details = '';
  meet.value.email = '';
  meet.value.tel = '';
  meet.value.placeStudy = '';
  localStorage.setItem('meets', JSON.stringify(meets.value));


}
const editMeet = (index) => {
  meet.value = { ...meets.value[index] };
  meet.value.editIndex = index;
};

const saveEdit = () => {
  meets.value[meet.value.editIndex] = { ...meet.value };
  meet.value.editIndex = undefined;
  meet.value = {};
  localStorage.setItem('meets', JSON.stringify(meets.value));
};
const deleteMeet = (index) => {
  meets.value.splice(index, 1);
  localStorage.setItem('meets', JSON.stringify(meets.value));
  selectedMeet.value = null
}
const handleMeetClick = (index) => {
  selectedMeet.value = selectedMeet.value === index ? null : index;
};
const handleEmailClick = (email) => {
  window.location.href = `mailto:${email}`;
}


</script>

<template>
  <div>
    <form>
      <label for="name">שם</label>
      <input type="text" id="name" v-model="meet.name"/><br />
      <label for="date">תאריך</label>
      <VueDatePicker v-model="meet.date" multi-dates />
      <label for="placeStudy">מקום לימודים</label>
      <input type="text" name="placeStudy" id="placeStudy" v-model="meet.placeStudy">
      <label for="email">מייל</label>
      <input type="email" name="email" id="email" v-model="meet.email">
      <input type="tel" name="tel" id="tel" v-model="meet.tel"><label for="tel">טלפון</label><br>
      <label for="details">פרטים</label>
      <textarea id="details" v-model="meet.details" dir="rtl"></textarea><br />
      <button v-if="selectedMeet === null" type="button" @click="addMeet">סיים</button>
    </form>
    <div class="meet-container">
      <div v-for="(meet, index) in meets" :key="index" class="meet-card">
        <div class="card-header">
          <MeetInfo @click="handleMeetClick(index)" :name="meet.name" :date="meet.date" />
          <div v-show="new Date().getDate() === 30" class="reminder">אל תשכח לשלוח דוח סיכום ודרישת תשלום למייל היום</div>
          <div v-if="selectedMeet === index" class="selected-meet" style="border:1px solid #000000">
            <MeetInfo @click="handleMeetClick(index)" :name="meet.name" :date="meet.date" />
           <div class="title1"><h2>מקום לימודים</h2> </div>
            <div class="title-line1"></div>
           
            <PlaceSudy :placeStudy="meet.placeStudy" />
            <div class="title2"><h2>סיכום פגישה</h2></div>
            <div class="title-line2"></div>
            <MeetDetails @click="handleMeetClick(index)" :details="meet.details" style="border: 1px;" />

            <MeetEmail :email="meet.email" @click="handleEmailClick(meet.email)" :tel="meet.tel" />
            <!-- <font-awesome-icon icon="envelope" @click="handleEmailClick(meet.email)" /> -->

            <div class="actions">
              <button @click="deleteMeet(index)">מחק</button>
              <button @click="editMeet(index)">ערוך</button>
              <button @click="saveEdit">שמור עריכה</button>

            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<style scoped>
.meet-container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
.title1{
  position: absolute;
  top: 60px;
  left: 70px;
}
.title-line1 {
  position: relative;
  width: 100%;
  height: 0;
  border-top: 2px solid #2a2020;
  top: 15px;
  /* background-color: #2a2020; */
  /* margin: 5px 0; */
}
.title2{
  position: absolute;
  top: 150px;
  left: 70px;
}
.title-line2 {
  position: relative;
  width: 100%;
  height: 0;
  border-top: 2px solid #2a2020;
  /* background-color: #2a2020; */
  top: 15px;
  /* margin: 5px 0; */
}

.meet-card {
  border: 1px solid #ddd;
  background-color: #ffffff;
  transition: transform 0.3s;
  flex: 1 0 calc(33.3333% - 20px);
  position: relative;
}

.card-header {
  padding: 10px;

}
#myCanvas {
  border: 1px;
}

.selected-meet {
  position: absolute;
  top: 70%;
  left: 50%;
  transform: translateX(-50%) scale(1.2);
  padding: 10px 20px;
  border: 1px solid #0000;
  display: flex;
  flex-direction: column;
  background-color: rgb(187, 242, 223);
  align-items: center;
  z-index: 2;
  display: grid;
  grid-template-rows: auto 1fr auto;
  gap: 10px;
  align-items: center;
}

.actions {
  display: flex;
  gap: 10px;
  justify-content: center;
}</style>
