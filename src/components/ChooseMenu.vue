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

        <v-btn v-if="selectionView === 'dinner'" class="py-4" @click="pickDinner(dinnerCook)"> Choose Dinner </v-btn>
        <v-btn v-else class="py-4" @click="pickDate()"> Choose Date </v-btn>

        <v-select
          v-model="seeMenu"
          class="py-4"
          label="See Choices"
          :items="opts"
          item-title="title"
          item-value="value"
          variant="solo-filled"
        />

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

const dinOpts = [
  { title: 'Cook', value: true },
  { title: 'TakeOut', value: false },
  { title: 'Either', value: 'Either' },
]

const opts = [
  { title: 'Yes', value: true },
  { title: 'No', value: false },
]

let tempArr = ref([])

function pickDinner(dinnerCook) {

  if (dinnerCook === 'Either') {

    console.log(dinnerCook)

    tonightDinner.value = dinnerIdeas.value[Math.floor(Math.random() * dinnerIdeas.value.length)].name
  } else if ((dinnerCook === true)) {
    for (let i = 0; i < dinnerIdeas.value.length; i++) {
      if ((dinnerIdeas.value[i].cook === true)) {
        console.log(dinnerIdeas.value[i].cook)
        tempArr.push(dinnerIdeas.value[i].name)
      }
      tonightDinner.value = tempArr.value[Math.floor(Math.random() * tempArr.value.length)]
    }
    tonightDinner.value = tempArr.value[Math.floor(Math.random() * tempArr.value.length)]
  } else {
  }
}

function pickDate() {
  tonightOption.value = dateIdeas.value[Math.floor(Math.random() * dateIdeas.value.length)].name
}
</script>

<style>
h3 {
  margin: auto;
  color: rgb(9, 39, 102);
  font-size: 19px;
}
</style>
