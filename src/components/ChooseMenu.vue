<template>
  <div>
    <h2>Picking</h2>
    <v-select
      v-model="selectionView"
      label="Select"
      :items="items"
      item-title="title"
      item-value="value"
      variant="solo-filled"
    ></v-select>
    


    <v-btn v-if="selectionView === 'dinner'" @click="pickDinner()"
      >Choose Dinner</v-btn
    >
    <v-btn v-else-if="selectionView === 'date'" @click="pickDate()"
      >Choose Date</v-btn
    >

    <h3 v-if="selectionView==='dinner'">Tonight's Dinner: {{ tonightDinner }}</h3>
    <h3 v-if="selectionView==='date'">Tonight's date: {{ tonightOption }}</h3>
  </div>
</template>
<script setup>
import { ref } from "vue";


const dinner = ["chicken", "death", "kebabs"];
const date = ["movie", "restaurant", "arcade"];
let tonightDinner = ref(" ");
let tonightOption = ref(" ");
const items = [
  { title: "Dinner", value: "dinner" },
  { title: "Date", value: "date" },
];
let selectionView = "dinner";

function pickDinner() {
  tonightDinner.value = dinner[Math.floor(Math.random() * dinner.length)];
}

function pickDate() {
  tonightOption.value = date[Math.floor(Math.random() * date.length)];
}
</script>

<style>
h3{
  margin: auto;
  color: rgb(9, 39, 102);
  font-size: 18px;
}
</style>
