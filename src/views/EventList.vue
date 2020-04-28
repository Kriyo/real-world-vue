<template>
  <div>
    <h1>Events Listing</h1>
    <EventCard v-for="event in events" :event="event" :key="event.id" />
    <template v-if="page !== 1">
      <router-link
        :to="{ name: 'event-list', query: { page: page -1 } }"
        rel="prev"
      >Prev Page |&nbsp;</router-link>
    </template>
    <router-link :to="{ name: 'event-list', query: { page: page +1 } }" rel="next">Next Page</router-link>
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
    this.$store.dispatch('fetchEvents', {
      perPage: 3,
      page: this.page
    })
  },
  computed: {
    page() {
      return parseInt(this.$route.query.page) || 1 // check for query param, fallback assumption to first page.
    },
    ...mapState(['events'])
  }
}
</script>
