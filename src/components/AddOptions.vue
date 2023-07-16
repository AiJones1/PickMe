<template>
  <v-card>
    <div class="py-5 px-5" 
    id="myDiv">
    <h2>Add Your Own Favourites!</h2>

    <v-select></v-select>
    
    <v-text-field
      v-model="input"
      label="Type Here"
      @keydown.enter="addDinner(input)"
    />
    <v-btn @click="addDinner(input)">
      Add your favourite meals
    </v-btn>
  </div>
  </v-card>
  
</template>

<script setup>
import { ref } from "vue";
const input = ref("");

function addDinner(din) {
  dinner.push(din);
  set(input, "");
}
</script>

<style>
h2{
  margin: auto;
  font-size: 20px;

}
</style>
