<template>
  <Header />
  <div class="container position-relative rounded-lg d-flex flex-column pt-15">
    <div class="d-flex mt-4">
      <Card
        number="4"
        title="صفحه"
        text="سا 3-4 هفته از کار خود صرفه جویی کنید"
      />
      <Card
        number="+15"
        title="طراحی بلاک"
        text="هنگامی که از صفحات از پیش ساخته شده استفاده می کنید، 3-4 هفته از کار خود صرفه جویی کنید"
      />
      <Card
        number="+70"
        title="المنت"
        text="هنگامی که از صفحات از پیش ساخته شده استفاده می کنید، 3-4 هفته از کار خود صرفه جویی کنید"
      />
    </div>
    <div class="px-15 mt-15 mb-10">
      <div v-if="isLoading">Loading ...</div>
      <Table v-else :events="events" />
    </div>
  </div>
</template>

<script lang="ts" setup>
import { onMounted } from 'vue'
import EventService from '@/services/EventService';

const events = ref([])
const isLoading = ref(true)

onMounted(() => {
    EventService.getEvents()
    .then((response:any) => {
        // console.log('events => ', response.data)
        events.value = response.data
        
    })
    .catch((error:any) => {
        console.log('error event => ', error )

    })
    .finally(() => {
      isLoading.value = false
    })
})

</script>
<style scoped>
.container {
  background-color: rgba(241, 246, 241, 0.92);
  top: -4%;
  width: 95vw;
  margin: 0px auto;
  box-shadow: 1px 1px 14px 0px;
}
</style>
