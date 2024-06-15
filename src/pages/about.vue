<template>
  <div>about page</div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService';

const events = ref(null)
console.log('test')
onMounted(() => {
    EventService.getEvents()
    .then((response) => {
        console.log('elyas: ', response.data)
    })
    .catch((error) => {
        console.log('error:', error )
    })
})



</script>

<style>

</style>