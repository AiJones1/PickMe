<template>
  <div class="w-full">
    <v-card>
      <div class="py-4 px-4">
        <h3 class="pb-8">
          Picking
        </h3>
        <v-select
          v-model="selectionView"
          label="Select"
          :items="items"
          item-title="title"
          item-value="value"
          variant="solo-filled"
        />

        <v-btn
          v-if="selectionView === 'dinner'"
          class="py-4"
          @click="pickDinner()"
        >
          Choose Dinner
        </v-btn>
        <v-btn
          v-else
          class="py-4"
          @click="pickDate()"
        >
          Choose Date
        </v-btn>
        <v-select
          v-model="seeMenu"
          class="py-4"
          label="See Choices"
          :items="opts"
          item-title="title"
          item-value="value"
          variant="solo-filled"
        />

        <h3 v-if="selectionView === 'dinner'">
          Tonight's Dinner: {{ tonightDinner }}
        </h3>
        <h3 v-else>
          Tonight's date: {{ tonightOption }}
        </h3>

        <div
          v-if="seeMenu"
          class="pt-12"
        >
          <div v-if="selectionView === 'dinner'">
            <h3>Dinner Options</h3>
            <v-list v-if="seeMenu">
              <v-list-item
                v-for="dinner in dinnerIdeas"
                :key="dinner"
              >
                {{ dinner }}
              </v-list-item>
            </v-list>
          </div>
          <div v-if="selectionView === 'date'">
            <h3>Date Options</h3>
            <v-list v-if="seeMenu">
              <v-list-item
                v-for="date in dateIdeas"
                :key="date"
              >
                {{ date }}
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
  'Chicken Katsu Curry',
  'Frozen Pizza',
  'Kebabs',
  'Hot Pot',
  'Dominos',
  'Greek Takeout',
  'Chinese Food',
  'KFC',
  'Pork Belly',
  'Pad Thai Chicken',
  'Burgers',
  'Salmon and Cous Cous',
  'HSP',
])
const dateIdeas = ref([
  'Cinemas',
  'Restaurant',
  'Arcade',
  'Beach Picnic',
  'Bottomless Brunch',
  'Movie Drinking Game',
  'Bar hopping',
  'Spa night',
])
let tonightDinner = ref(' ')
let tonightOption = ref(' ')
const items = [
  { title: 'Dinner', value: 'dinner' },
  { title: 'Date', value: 'date' },
]
let selectionView = ref('dinner')
let seeMenu = ref(false)

const opts = [
  { title: 'Yes', value: true },
  { title: 'No', value: false },
]

function pickDinner() {
  tonightDinner.value = dinnerIdeas.value[Math.floor(Math.random() * dinnerIdeas.value.length)]
}

function pickDate() {
  tonightOption.value = dateIdeas[Math.floor(Math.random() * dateIdeas.value.length)]
  tonightOption.value = dateIdeas.value[Math.floor(Math.random() * dateIdeas.value.length)]
}

// function dinnerMenu() {
//   console.log(dinner);

//   for (const i = 0; i < dinner.size; i++) {
//     dinner(i);
//     console.log(dinner(i));
//   }
// }

// function dateMenu() {
//   console.log(date.toString);
// }
</script>

<style>
h3 {
  margin: auto;
  color: rgb(9, 39, 102);
  font-size: 18px;
}

</style>
