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
  <h2>{{opt2Dinner}}</h2>
  <h2>{{opt3Dinner}}</h2>
  <div v-if="seeMenu" class="pt-12">
    <h3>Dinner Options</h3>
    <v-list>
      <v-list-item v-for="dinner in filteredDinnerIdeas" :key="dinner">
        {{ dinner.name }}
      </v-list-item>
    </v-list>
  </div>
</template>

<script setup>
import { ref , computed} from 'vue'
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
let opt2Dinner = ref('')
let opt3Dinner = ref('')

const dinOpts = [
  { title: 'Quick', value: 'Quick' },
  { title: 'Long', value: 'Long' },
  { title: 'New', value: 'New' },
  { title: 'Anything', value: 'Either' },
]

const filteredDinnerIdeas = computed(()=>{
  return filterPreference(dinnerCook.value, dinnerIdeas)
})

// functions
function pickDinner(dinnerCook) {
  opt2Dinner = ref('')
  opt3Dinner = ref('')
  tonightDinner.value = pickRandom(filterPreference(dinnerCook, dinnerIdeas)).name
}

 function threeOptions(dinnerCook){
  const filteredOptions = filterPreference(dinnerCook, dinnerIdeas)
  tonightDinner.value =pickRandom(filteredOptions).name
    
    let remainingOptions = filteredOptions.filter(option=> option.name!=tonightDinner.value)
    opt2Dinner.value=pickRandom(remainingOptions1).name
    

    remainingOptions = remainingOptions.filter(option=> option.name!=opt2Dinner.value)
    opt3Dinner.value=pickRandom(remainingOptions).name
}

function pickRandom(array) {
  return array[Math.floor(Math.random() * array.length)]
}

function filterPreference(dinnerCook, array){
    if(dinnerCook==='Either'){
      return array.value
    }else if(dinnerCook==='Quick'){
      return array.value.filter((idea)=> idea.cook==='Quick')
    }else if(dinnerCook==='Long'){
      return array.value.filter((idea)=> idea.cook==='Long')
    }else{
      return array.value.filter((idea)=>idea.cook==='New')
    }
}
</script>

<style></style>
