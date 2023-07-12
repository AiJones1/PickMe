<template>
  <div>
    <v-btn @click="toggleView()">Toggle View</v-btn>
    <choose-menu v-if="view === 0"></choose-menu>

    <add-options v-else> </add-options>
  </div>
</template>
<script setup>
import { ref } from "vue";
import AddOptions from "./AddOptions.vue";
import ChooseMenu from "./ChooseMenu.vue";

// reactive state

const view = ref(0);

function toggleView() {
  view.value = view.value === 0 ? 1 : 0;
}

// lifecycle hooks
</script>

<style></style>
