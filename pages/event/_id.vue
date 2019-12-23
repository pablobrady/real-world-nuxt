<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'What you need to know about event ' + this.event.title
        }
      ]
    }
  },
  async fetch({ store, error, params }) {
    try {
      await store.dispatch('events/fetchEvent', params.id )
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch event #' + params.id + '.  Sorry dude, dudess, or non-binary dude-person.'
      })
    }
  },
  computed: mapState({
    event: state => state.events.event
  })
}
</script>
