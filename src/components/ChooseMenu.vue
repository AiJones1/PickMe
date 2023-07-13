<template>
  <div class="pt-8">
    <v-col cols="12">
      <v-card>
        <div class="py-4 px-4">
          <h2 class="pb-8">
            Picking
          </h2>
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

        <!-- <h2>Dinner Options</h2>
    <v-list v-if="seeMenu">
      <v-list-item
        v-for="dinner in dinnerIdeas"
        :key="dinner"
      >
        {{ dinner }}
      </v-list-item>
    </v-list>
    <h3>Date Options</h3>
    <v-list v-if="seeMenu">
      <v-list-item
        v-for="date in dateIdeas"
        :key="date"
      >
        {{ date }}
      </v-list-item>
    </v-list> -->
        </div>
      </v-card>
    </v-col>
  </div>
</template>
<script setup>
import { ref } from 'vue'

const dinner = [
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
]
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
  tonightDinner.value = dinner[Math.floor(Math.random() * dinner.length)]
}

function pickDate() {
  tonightOption.value = date[Math.floor(Math.random() * date.length)]
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
