<template>
  <div>about page</div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const events = ref(null)
console.log('test')
onMounted(() => {
    axios.get(
        'https://my-json-server.typicode.com/code-pop/real-world_vue-3/events'
    )
    .then((response) => {
        events.value = response.data
        console.log('events: ', response.data)
    })
    .catch((error) => {
        console.log('error:', error )
    })
})



</script>

<style>

</style>