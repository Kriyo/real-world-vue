<template>
  <div>
    <h1>Create an Event, {{ user.name }}</h1>
    <p>This event was created by {{ user.name }}</p>
    <p>{{ getEventById(1) }}</p>
    <p>There are {{ catLength }} categories</p>
    <ul>
      <li v-for="c in categories" :key="c">
        {{ c }}
      </li>
    </ul>
  </div>
</template>

<script>
import { mapState, mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters(['getEventById', 'catLength']),
    ...mapState(['user', 'categories'])
  }
}
</script>

<style lang="scss" scoped></style>
