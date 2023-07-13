<template>
  <div>
    <v-btn @click="toggleView()">
      Toggle View
    </v-btn>
    <choose-menu v-if="view === 0" />

    <add-options v-else />
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
