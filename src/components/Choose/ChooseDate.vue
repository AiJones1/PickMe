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
    <h3 class="pt-6">Tonight's Date: {{ tonightOption }}</h3>
    <div v-if="seeMenu"  class="pt-12">
      <h3>Date Options</h3>
      <v-list >
        <v-list-item v-for="date in dateIdeas" :key="date">
          {{ date.name }}
        </v-list-item>
      </v-list>
    </div>
  </div>
</template>

<script setup>
//props
const props = defineProps({ seeMenu: Boolean })

const dateOpts = [
  { title: 'Any Cost', value: 4 },
  { title: 'Expensive', value: 3 },
  { title: 'Spenny', value: 2 },
  { title: 'Cheap', value: 1 },
  { title: 'Free', value: 0 },
]

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

// functions

function pickDate(dateBudget) {
  switch (dateBudget) {
    case 4:
    case 3:
      tonightOption.value = pickRandom(dateIdeas.value).name
      break
    case 2:
      const spennyDates = dateIdeas.value.filter((idea) => idea.cost <= 2)
      tonightOption.value = pickRandom(spennyDates).name
      break
    case 1:
      const cheapDates = dateIdeas.value.filter((idea) => idea.cost <= 1)
      tonightOption.value = pickRandom(cheapDates).name
      break
    case 0:
      const freeDates = dateIdeas.value.filter((idea) => idea.cost <= 0)
      tonightOption.value = pickRandom(freeDates).name
      break
  }
}

function pickRandom(array) {
  return array[Math.floor(Math.random() * array.length)]
}
</script>

<style></style>
