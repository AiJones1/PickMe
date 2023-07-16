<template>
  <v-select
    v-model="dinnerCook"
    label="Specify"
    :items="dinOpts"
    item-title="title"
    item-value="value"
    variant="solo-filled"
  />
  <v-btn class="py-4" @click="pickDinner(dinnerCook)"> Choose Dinner </v-btn>
  <v-spacer/>
  <h3>Tonight's Dinner: {{ tonightDinner }}</h3>
  <div v-if="seeMenu" class="pt-12">
    <h3>Dinner Options</h3>
    <v-list>
      <v-list-item v-for="dinner in dinnerIdeas" :key="dinner">
        {{ dinner.name }}
      </v-list-item>
    </v-list>
  </div>
</template>

<script setup>
import { ref } from 'vue'
//props
const props = defineProps({ seeMenu: Boolean })

// refs
let dinnerCook = ref('Either')
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
let tonightDinner = ref('')
const dinOpts = [
  { title: 'Cook', value: true },
  { title: 'TakeOut', value: false },
  { title: 'Either', value: 'Either' },
]

// functions
function pickDinner(dinnerCook) {
  if (dinnerCook === 'Either') {
    tonightDinner.value = pickRandom(dinnerIdeas.value).name
  } else if (dinnerCook) {
    const cookableItems = dinnerIdeas.value.filter((idea) => idea.cook)
    tonightDinner.value = pickRandom(cookableItems).name
  } else {
    const nonCookableItems = dinnerIdeas.value.filter((idea) => !idea.cook)
    tonightDinner.value = pickRandom(nonCookableItems).name
  }
}

function pickRandom(array) {
  return array[Math.floor(Math.random() * array.length)]
}
</script>

<style></style>
