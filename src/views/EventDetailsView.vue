<script setup>
import { ref, onMounted } from 'vue'
import EventServices from '../services/EventServices'

const props = defineProps({
  id: {
    required: true,
  },
})

const event = ref(null)

onMounted(() => {
  EventServices.getEvent(props.id)
    .then((response) => {
      event.value = response.data
    })
    .catch((error) => console.log(error))
})
</script>

<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.data }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>
