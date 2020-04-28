<template>
  <div>
    <h1>Events Listing</h1>
    <EventCard v-for="event in events" :event="event" :key="event.id" />
    <template v-if="page !== 1">
      <router-link :to="{ name: 'event-list', query: { page: page -1 } }" rel="prev">Prev Page</router-link>
    </template>

    <template v-if="isLastPage">&nbsp;|&nbsp;</template>

    <template v-if="isLastPage">
      <router-link :to="{ name: 'event-list', query: { page: page +1 } }" rel="next">Next Page</router-link>
    </template>
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
    this.perPage = 3
    this.$store.dispatch('fetchEvents', {
      perPage: this.perPage,
      page: this.page
    })
  },
  computed: {
    page() {
      return parseInt(this.$route.query.page) || 1 // check for query param, fallback assumption to first page.
    },
    isLastPage() {
      console.log('total e: ', this.totalEvents)
      console.log('this.page', this.page)
      console.log('perPage', this.perPage)
      console.log(
        '::> this.totalEvents > this.page * this.perPage: ',
        this.totalEvents > this.page * this.perPage
      )
      return this.totalEvents > this.page * this.perPage
    },
    ...mapState(['events', 'totalEvents'])
  }
}
</script>
