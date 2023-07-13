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
      ></v-select
    >

    <v-btn v-if="selectionView === 'dinner'" @click="pickDinner()"
      >Choose Dinner</v-btn
    >
    <v-btn v-else-if="selectionView === 'date'" @click="pickDate()"
      >Choose Date</v-btn
    >
    <v-select
      v-model="seeMenu"
      label="See Choices"
      :items="opts"
      item-title="title"
      item-value="value"
      variant="solo-filled">

 
    </v-select>

    <h3 v-if="selectionView === 'dinner'">
      Tonight's Dinner: {{ tonightDinner }}
    </h3>
    <h3 v-else-if="selectionView === 'date'">
      Tonight's date: {{ tonightOption }}
    </h3>

    <ul v-if="selectionView === 'dinner'" id="dinnerOptions">
      Dinner Options
      <li v-if="seeMenu ==='yes'" v-for="value in dinner">

        {{ value }}
      </li>
    </ul>
    <ul v-if="selectionView === 'date'" id="dateOptions">
      Date Options
      <li v-if="seeMenu ==='yes'" v-for="value in date">
        {{ value }}
      </li>
    </ul>
  </div>
</template>
<script setup>
import { ref } from "vue";

const dinner = [
  "Chicken Katsu Curry",
  "Frozen Pizza",
  "Kebabs",
  "Hot Pot",
  "Dominos",
  "Greek Takeout",
  "Chinese Food",
  "KFC",
  "Pork Belly",
  "Pad Thai Chicken",
  "Burgers",
  "Salmon and Cous Cous",
  "HSP",
];
const date = [
  "Cinemas",
  "Restaurant",
  "Arcade",
  "Beach Picnic",
  "Bottomless Brunch",
  "Movie Drinking Game",
  "Bar hopping",
  "Spa night",
];
let tonightDinner = ref(" ");
let tonightOption = ref(" ");
const items = [
  { title: "Dinner", value: "dinner" },
  { title: "Date", value: "date" },
];
let selectionView = "dinner";
let seeMenu = "no";

const opts =[
  {title: "Yes", value:"yes"},
  {title: "No", value: "no" }
]

function pickDinner() {
  tonightDinner.value = dinner[Math.floor(Math.random() * dinner.length)];
}

function pickDate() {
  tonightOption.value = date[Math.floor(Math.random() * date.length)];
}

function dinnerMenu() {
  console.log(dinner);

  for (const i = 0; i < dinner.size; i++) {
    dinner(i);
    console.log(dinner(i));
  }
}

function dateMenu() {
  console.log(date.toString);
}
</script>

<style>
h3 {
  margin: auto;
  color: rgb(9, 39, 102);
  font-size: 18px;
}
</style>
