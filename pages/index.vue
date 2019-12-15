<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue';
export default {
  head() {     // vue-meta property
    return {
      title: 'Event Listing'  // default description will be inherited
    }
  },
  async asyncData({ $axios, error = null }) {
    try {
      const { data } = await $axios.get('http://localhost:3000/events')
      return {
        events: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time.  Sorry dude, dudess, or non-binary dude-person.'
      })
    }
  },
  components: {
    EventCard
  }
}
</script>
