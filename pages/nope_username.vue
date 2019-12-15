<template>
  <div>
    <h1>Username is {{ username }}</h1>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: 'Username ' + this.username,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.username + ': member in since 1980.'
        }
      ]
    }
  },
  computed: {
    username() {
      return this.$route.params.username
    }
  }
}
</script>
