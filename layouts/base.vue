<template>
  <v-app dark :style="customStyle">
    <slot name="header" />
    <v-content>
      <slot />
    </v-content>
    <slot name="footer" />
  </v-app>
</template>

<script>
export default {
  computed: {
    customStyle () {
      return this.$route.query.modal ? { background: 'rgba(55, 58, 60, 0.4)' } : {}
    }
  },
  head () {
    return this.$store.state.policies.discourage_index ? {
      meta: [
        { name: 'robots', content: 'noindex' }
      ]
    } : {}
  }
}
</script>
