<template>
  <div>
    <v-row justify="center">
      <v-btn
        class="mb-12"
        @click="toggleView()"
      >
        Toggle View
      </v-btn>
    </v-row>
    <choose-menu v-if="view === 0" />
    <add-options v-else />
  </div>
</template>
<script setup>
import { ref } from "vue";
import AddOptions from "./AddOptions.vue";
import ChooseMenu from "./Choose/ChooseMenu.vue";

//refs
const view = ref(0);

//methods
function toggleView() {
  view.value = view.value === 0 ? 1 : 0;
}
</script>

