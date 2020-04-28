<template>
  <div v-if="events">
    <h1>Events Listing</h1>
    <EventCard v-for="event in events" :event="event" :key="event.id" />
    <BaseIcon />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
import { mapState } from 'vuex'

export default {
  components: {
    EventCard
  },
  created() {
    this.$store.dispatch('fetchEvents')
  },
  computed: mapState(['events'])
}
</script>
