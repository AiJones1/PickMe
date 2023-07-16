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

function pickDinner(dinnerCook) {
  if (dinnerCook === 'Either') {
    tonightDinner.value = pickRandom(dinnerIdeas.value).name
  } else if (dinnerCook) {
    const cookableItems = dinnerIdeas.value.filter(idea=>idea.cook)
    tonightDinner.value = pickRandom(cookableItems).name
  } else {
    const nonCookableItems = dinnerIdeas.value.filter(idea=> !idea.cook)
    tonightDinner.value = pickRandom(nonCookableItems).name
  }
}

function pickDate(dateBudget) {

  switch(dateBudget){
    case 4:
    case 3:
      tonightOption.value = pickRandom(dateIdeas.value).name
      break;
    case 2:
      const spennyDates=  dateIdeas.value.filter(idea=> idea.cost<=2)
      tonightOption.value =  pickRandom(spennyDates).name
      break;
    case 1:
      const cheapDates = dateIdeas.value.filter(idea=> idea.cost<=1)
      tonightOption.value =  pickRandom(cheapDates).name
      break;
    case 0:
      const freeDates = dateIdeas.value.filter(idea=> idea.cost <=0)
      tonightOption.value =  pickRandom(freeDates).name
      break;
  }
}

// Helpers

function pickRandom(array) {
  return array[Math.floor(Math.random() * array.length)]
}
</script>

<style>
h3 {
  margin: auto;
  color: rgb(9, 39, 102);
  font-size: 19px;
}
</style>
