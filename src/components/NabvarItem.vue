<template>
  <v-btn color="blue-grey-darken-2">
      <v-icon>mdi-menu-down</v-icon>
      <span>{{ props.name }}</span>
      <v-icon class="ml-1">mdi-{{ props.icon }}</v-icon>

  </v-btn>
</template>

<script setup lang="ts">
const props = defineProps(["name", "icon", "to"]);
</script>

<style>
</style>