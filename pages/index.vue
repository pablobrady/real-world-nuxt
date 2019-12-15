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
  asyncData({ $axios, error }) {   // accepts "context" var, or this es6 shortcut $axios
    return $axios.get('http://localhost:3000/events').then( response => {
      return {
        events: response.data       // Returns the component data directly. (No manual data merging.)
      }
    })
    .catch(e => {
      if( e ) { null }
      error({
        statusCode: 503, message: 'Unable to fetch events at this time.  Please try again. '
      })
    })
  },
  components: {
    EventCard
  }
}
</script>
