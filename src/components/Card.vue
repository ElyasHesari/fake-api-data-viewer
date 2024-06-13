<template>
  <v-card
    variant="variant"
    class="mx-auto d-flex flex-column text-center"
    color="light"
    max-width="344"
    
  >
    <div class="number">{{ props.number }}</div>
    <v-card-title>{{ props.title }}</v-card-title>
    <v-card-subtitle class="mt-2">
        {{ props.text }}
    </v-card-subtitle>
  </v-card>
</template>

<script setup>
const props = defineProps(["number", "title", "text"]);
</script>

<style scoped>
.number {
    font-size: 48px;
    color: #4caf50;
}
</style>