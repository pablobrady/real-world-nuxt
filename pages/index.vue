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
import EventService from '@/services/EventService.js'

export default {
  head() {     // vue-meta property
    return {
      title: 'Event Listing'  // default description will be inherited
    }
  },
  async asyncData({ error = null }) {
    try {
      const { data } = await EventService.getEvents()
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
