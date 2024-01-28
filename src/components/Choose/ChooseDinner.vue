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
  <v-btn class="py-4" @click="threeOptions(dinnerCook)">Three Options</v-btn>

  <h3 class="pt-6">Tonight's Dinner: </h3>
  <h2>{{tonightDinner}}</h2>
  <h2>{{longDinner}}</h2>
  <h2>{{newDinner}}</h2>
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
  { name: 'Chicken Katsu Curry', cook: 'Quick' },
  { name: 'Hot Pot', cook: 'Quick'},
  { name: 'Pad Thai Chicken', cook: 'Quick' },
  { name: 'Stacked Burgers', cook: 'Quick' },
  { name: 'Salmon', cook: 'Quick' },
  { name: 'Fried Chicken Burger', cook: 'Quick'},
  {name: 'Soupy Noodles', cook: 'Quick'},
  {name: 'Stroganov', cook: 'Quick'},
  {name: 'Egg Noodles', cook: 'Quick'},
  {name: 'Cali Burrito', cook: 'Quick'},
  {name: 'Fried Rice', cook: 'Quick'},
  {name: 'Beef Noodle Stir Fry', cook: 'Quick'},
  {name: 'Chicken and Chip Rolls', cook: 'Quick'},

  {name:'Pork Belly', cook: 'Long'},
  {name:'Sweet and Sour Pork', cook: 'Long'},

  {name: 'Wontons', cook: 'New'}, 
  {name: 'Ginger Steamed Fish', cook: 'New'}, 
  {name: 'Honey Soy Chicken', cook: 'New'}, 
])

let tonightDinner = ref('')
let longDinner = ref('')
let newDinner = ref('')

const dinOpts = [
  { title: 'Quick', value: 'Quick' },
  { title: 'Long', value: 'Long' },
  { title: 'New', value: 'New' },
  { title: 'Either', value: 'Either' },
]

// functions
function pickDinner(dinnerCook) {
 longDinner = ref('')
 newDinner = ref('')
  if (dinnerCook === 'Either') {
    tonightDinner.value = pickRandom(dinnerIdeas.value).name
  } else if (dinnerCook==='Quick') {
    // const easyCookableItems = dinnerIdeas.value.filter((idea) => idea.cook==='Quick')

    tonightDinner.value = pickRandom(filterQuick(dinnerIdeas)).name
  } else if(dinnerCook==='Long'){
    const hardCookableItems = dinnerIdeas.value.filter((idea) => idea.cook==='Long')
    tonightDinner.value = pickRandom(hardCookableItems).name
  } else{
    const newCookableItems = dinnerIdeas.value.filter((idea)=> idea.cook==='New')
    tonightDinner.value = pickRandom(newCookableItems).name

  }
}

 function threeOptions(dinnerCook){
    tonightDinner.value =pickRandom(filterQuick(dinnerIdeas)).name
    longDinner.value=pickRandom(filterLong(dinnerIdeas)).name
    newDinner.value=pickRandom(filterNew(dinnerIdeas)).name
}

function pickRandom(array) {
  return array[Math.floor(Math.random() * array.length)]
}

function filterQuick(array){
  return array.value.filter((idea)=> idea.cook==='Quick')
}
function filterLong(array){
  return array.value.filter((idea)=> idea.cook==='Long')
}
function filterNew(array){
  return array.value.filter((idea)=>idea.cook==='New')
}
</script>

<style></style>
