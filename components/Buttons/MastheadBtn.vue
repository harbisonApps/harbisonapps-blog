<template>
  <v-btn
    :to="to"
    color="secondary"
    exact
    height="75"
    width="300"
    nuxt
    dark
    class="px-12 text-h5 text-capitalize"
  >
    {{ text }}
  </v-btn>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      required: true
    },
    to: {
      type: String,
      required: true
    }
  }
}
</script>

<style scoped>
/* .v-btn__content {
  color: black;
} */
</style>
