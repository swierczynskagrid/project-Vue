<script setup>
// import EventCard from './components/EventCard.vue'
import EventCard from '@/components/EventCard.vue' //@ makes it an absolute path
import { ref, onMounted } from 'vue'
import EventServices from '../services/EventServices'

const events = ref(null)

onMounted(() => {
  EventServices.getEvents()
    .then((response) => {
      events.value = response.data
    })
    .catch((error) => console.log(error))
})
</script>

<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
