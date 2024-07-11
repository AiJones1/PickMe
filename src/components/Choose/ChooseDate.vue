<template>
  <div>
    <v-select
      v-model="dateBudget"
      label="Specify"
      :items="dateOpts"
      item-title="title"
      item-value="value"
      variant="solo-filled"
    />
    <v-btn class="py-4" @click="pickDate(dateBudget)"> Choose Date </v-btn>
    <v-btn class="py-4" @click="threeChoices(dateBudget)">Three Options</v-btn>
    <h3 class="pt-6">Tonight's Date:</h3>
    <h2> {{ tonightOption }}</h2>
    <h2> {{ opt2Date }}</h2>
    <h2> {{ opt3Date }}</h2>
    <div v-if="seeMenu"  class="pt-12">
      <h3>Date Options</h3>
      <v-list >
        <v-list-item v-for="date in filteredDateIdeas" :key="date">
          {{ date.name }}
        </v-list-item>
      </v-list>
    </div>
  </div>
</template>

<script setup>
import { ref , computed} from 'vue'

//props
const props = defineProps({ seeMenu: Boolean })

// refs
let dateBudget = ref(4)
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

let tonightOption = ref('')
let opt2Date = ref('')
let opt3Date = ref('')

const dateOpts = [
  { title: 'Any Cost', value: 4 },
  { title: 'Expensive', value: 3 },
  { title: 'Spenny', value: 2 },
  { title: 'Cheap', value: 1 },
  { title: 'Free', value: 0 },
]

const filteredDateIdeas = computed(()=>{
  return filterDates(dateBudget.value, dateIdeas)
})
// functions

function pickDate(dateBudget) {
  opt2Date = ref('')
  opt3Date = ref('')
  tonightOption.value=pickRandom(filterDates(dateBudget,dateIdeas)).name
}

function threeChoices(dateBudget){
  const filteredDates = filterDates(dateBudget, dateIdeas)
  tonightOption.value=pickRandom(filteredDates).name

  let remainingDates = filteredDates.filter((opt)=> opt.name!=tonightOption.value)
  opt2Date.value = pickRandom(remainingDates).name

  remainingDates = remainingDates.filter((opt)=> opt.name!=opt2Date.value)
  opt3Date.value = pickRandom(remainingDates).name
}

function pickRandom(array) {
  return array[Math.floor(Math.random() * array.length)]
}

function filterDates(dateBudget, array){
  if(dateBudget===4){
    return array.value
  }else if(dateBudget===3){
    return array.value.filter((opt)=> opt.cost===3)
  }else if(dateBudget===2){
    return array.value.filter((opt)=> opt.cost===2)
  }else if(dateBudget>=1){
    return array.value.filter((opt)=> opt.cost===1)
  }else{
    return array.value.filter((opt)=> opt.cost===0)
}
}
</script>

<style></style>
