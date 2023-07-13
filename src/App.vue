<template>
  <title>Pick 4 Me</title>
  <h1>
    Pick 4 Me
    <Icon
      icon="fluent-emoji-flat:wheel"
      width="44"
      height="44"
    />
  </h1>
  <main>
    <picking />
  </main>
</template>

<script setup>
import Picking from './components/Picking.vue'
import { Icon } from '@iconify/vue'
</script>

<style scoped>
h1 {
  margin: 0 auto;
  color: rgb(85, 4, 85);
  font-size: 40px;
  font-display: block;
}
</style>
