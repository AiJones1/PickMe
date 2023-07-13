<template>
  <div id="myDiv">
    <h2>This is toggling display</h2>
    
    <v-text-field
      v-model="input"
      label="add your own favourite options!"
      @keydown.enter="addDinner(input)"
    />
    <v-btn @click="addDinner(input)">
      Add your favourite meals
    </v-btn>
  </div>
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
