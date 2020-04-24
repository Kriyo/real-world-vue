<template>
  <div>
    <h1>Events Listing</h1>
    <EventCard v-for="event in events" :event="event" :key="event.id" />
    <BaseIcon />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService.js'
export default {
  components: {
    EventCard
  },
  data() {
    return { events: [] }
  },
  created() {
    EventService.getEvents()
      .then(res => {
        this.events = res.data
      })
      .catch(error => {
        console.log('::> Errors:', error)
      })
  }
}
</script>
