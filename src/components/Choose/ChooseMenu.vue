<template>
  <div class="w-full">
    <v-card>
      <div class="py-4 px-4">
        <h3 class="pb-8">Picking</h3>
        <v-select
          v-model="selectionView"
          label="Select"
          :items="selectionItems"
          item-title="title"
          item-value="value"
          variant="solo-filled"
        />
        <v-switch v-model="seeMenu" label="See Choices" />
        <choose-date :see-menu="seeMenu" v-if="selectionView === 'date'"></choose-date>
        <choose-dinner :see-menu="seeMenu" v-if="selectionView === 'dinner'"></choose-dinner>
        </div>
    </v-card>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import ChooseDate from './ChooseDate.vue'
import ChooseDinner from './ChooseDinner.vue'

const selectionItems = [
  { title: 'Dinner', value: 'dinner' },
  { title: 'Date', value: 'date' },
]
let selectionView = ref('dinner')
let seeMenu = ref(false)
</script>

<style>
h3 {
  margin: auto;
  color: rgb(9, 39, 102);
  font-size: 19px;
}
</style>
