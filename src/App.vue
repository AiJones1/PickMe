<template>
  <v-container>
    <v-row
      class="flex justify-center"
    >
      <h1>Pick 4 Me</h1>
      <Icon
        icon="fluent-emoji-flat:wheel"
        width="44"
        height="44"
      />
    </v-row>
    <v-row justify="center">
      <picking />
    </v-row>
  </v-container>
</template>

<script setup>
import Picking from './components/Picking.vue'
import { Icon } from '@iconify/vue'
</script>

<style scoped>
h1 {
  color: rgb(85, 4, 85);
  font-size: 40px;
  font-display: block;
}
</style>
