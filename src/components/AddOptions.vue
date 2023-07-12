<template>
  <div id="myDiv">
    <h1>This is toggling display</h1>

    <v-text-field
      @keydown.enter="addDinner(input)"
      label="add your own favourite options!"
      v-model="input"
    ></v-text-field>
    <v-btn @click="addDinner(input)">Add your favourite meals</v-btn>
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
