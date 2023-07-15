<template>
  <div class="w-full">
    <v-card>
      <div class="py-4 px-4">
        <h3 class="pb-8">Picking</h3>
        <v-select
          v-model="selectionView"
          label="Select"
          :items="items"
          item-title="title"
          item-value="value"
          variant="solo-filled"
        />
        <v-select
          v-if="selectionView === 'dinner'"
          v-model="dinnerCook"
          label="Specify"
          :items="dinOpts"
          item-title="title"
          item-value="value"
          variant="solo-filled"
        />
        <v-select
          v-if="selectionView === 'date'"
          v-model="dateBudget"
          label="Specify"
          :items="dateOpts"
          item-title="title"
          item-value="value"
          variant="solo-filled"
        />

        <v-btn v-if="selectionView === 'dinner'" class="py-4" @click="pickDinner(dinnerCook)"> Choose Dinner </v-btn>
        <v-btn v-else class="py-4" @click="pickDate(dateBudget)"> Choose Date </v-btn>

        <v-switch v-model="seeMenu" label="See Choices" />

        <h3 v-if="selectionView === 'dinner'">Tonight's Dinner: {{ tonightDinner }}</h3>
        <h3 v-else>Tonight's date: {{ tonightOption }}</h3>

        <div v-if="seeMenu" class="pt-12">
          <div v-if="selectionView === 'dinner'">
            <h3>Dinner Options</h3>
            <v-list v-if="seeMenu">
              <v-list-item v-for="dinner in dinnerIdeas" :key="dinner">
                {{ dinner.name }}
              </v-list-item>
            </v-list>
          </div>
          <div v-if="selectionView === 'date'">
            <h3>Date Options</h3>
            <v-list v-if="seeMenu">
              <v-list-item v-for="date in dateIdeas" :key="date">
                {{ date.name }}
              </v-list-item>
            </v-list>
          </div>
        </div>
      </div>
    </v-card>
  </div>
</template>
<script setup>
import { ref } from 'vue'

const dinnerIdeas = ref([
  { name: 'Chicken Katsu Curry', cook: true },
  { name: 'Frozen Pizza', cook: true },
  { name: 'Kebabs', cook: false },
  { name: 'Hot Pot', cook: true },
  { name: 'Dominos', cook: false },
  { name: 'Greek Takeout', cook: false },
  { name: 'Chinese Food', cook: false },
  { name: 'KFC', cook: false },
  { name: 'Pork Belly', cook: true },
  { name: 'Pad Thai Chicken', cook: true },
  { name: 'Burgers', cook: true },
  { name: 'Salmon and Cous Cous', cook: true },
  { name: 'HSP', cook: false },
])
const dateIdeas = ref([
  { name: 'Cinemas', cost: 2 },
  { name: 'Restaurant', cost: 2 },
  { name: 'Arcade', cost: 1 },
  { name: 'Beach Picnic', cost: 0 },
  { name: 'Bottomless Brunch', cost: 3 },
  { name: 'Home Movie Drinking Game', cost: 1 },
  { name: 'Bar hopping', cost: 2 },
  { name: 'Spa night', cost: 0 },
])
let tonightDinner = ref(' ')
let tonightOption = ref(' ')
const items = [
  { title: 'Dinner', value: 'dinner' },
  { title: 'Date', value: 'date' },
]
let selectionView = ref('dinner')
let seeMenu = ref(false)
let dinnerCook = ref('Either')
let dateBudget = ref(4)
const dinOpts = [
  { title: 'Cook', value: true },
  { title: 'TakeOut', value: false },
  { title: 'Either', value: 'Either' },
]
const dateOpts = [
  { title: 'Any Cost', value: 4 },
  { title: 'Expensive', value: 3 },
  { title: 'Spenny', value: 2 },
  { title: 'Cheap', value: 1 },
  { title: 'Free', value: 0 },
]

let tempArr = ref([])

function pickDinner(dinnerCook) {
  if (dinnerCook === 'Either') {

    tonightDinner.value = dinnerIdeas.value[Math.floor(Math.random() * dinnerIdeas.value.length)].name
  } else if (dinnerCook === true) {
    for (let i = 0; i < dinnerIdeas.value.length; i++) {
      if (dinnerIdeas.value[i].cook === true) {
        tempArr.value.push(dinnerIdeas.value[i].name)
      }
    }
    tonightDinner.value = tempArr.value[Math.floor(Math.random() * tempArr.value.length)]
  } else {
    for (let j = 0; j < dinnerIdeas.value.length; j++) {
      if (dinnerIdeas.value[j].cook === false) {
        tempArr.value.push(dinnerIdeas.value[j].name)
      }
    }
    tonightDinner.value = tempArr.value[Math.floor(Math.random() * tempArr.value.length)]
  }
  tempArr.value = []
}

function pickDate(dateBudget) {
  if (dateBudget > 2) {
    tonightOption.value = dateIdeas.value[Math.floor(Math.random() * dateIdeas.value.length)].name
  } else if (dateBudget === 2) {
    for (let i = 0; i < dateIdeas.value.length; i++) {
      if (dateIdeas.value[i].cost <= 2) {
        tempArr.value.push(dateIdeas.value[i].name)
      }
    }
    tonightOption.value = tempArr.value[Math.floor(Math.random() * tempArr.value.length)]
  } else if (dateBudget === 1) {
    for (let j = 0; j < dateIdeas.value.length; j++) {
      if (dateIdeas.value[j].cost <= 1) {
        tempArr.value.push(dateIdeas.value[j].name)
      }
    }
    tonightOption.value = tempArr.value[Math.floor(Math.random() * tempArr.value.length)]
  } else {
    for (let k = 0; k < dateIdeas.value.length; k++) {
      if (dateIdeas.value[k].cost === 0) {
        tempArr.value.push(dateIdeas.value[k].name)
      }
    }
    tonightOption.value = tempArr.value[Math.floor(Math.random() * tempArr.value.length)]
  }
  tempArr = []
}
</script>

<style>
h3 {
  margin: auto;
  color: rgb(9, 39, 102);
  font-size: 19px;
}
</style>
