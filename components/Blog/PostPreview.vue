<template>
  <v-col
    cols="12"
    sm="6"
    md="4"
  >
    <v-card>
      <!-- eslint-disable-next-line vue/html-self-closing -->
      <v-img
        :src="thumbnail"
        class="white--text align-end"
        height="200px"
      ></v-img>
      <v-card-title class="pb-1">
        {{ title }}
      </v-card-title>
      <p class="pl-4 mb-n2 date">
        {{ date }}
      </p>
      <v-card-text class="text--primary">
        <div>{{ excerpt }}</div>
      </v-card-text>

      <v-card-actions class="ma-auto text-center">
        <v-btn
          :to="'/blog/' + id"
          nuxt
          block
          dark
          color="accent"
        >
          Read
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-col>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    excerpt: {
      type: String,
      required: true
    },
    thumbnail: {
      type: String,
      required: true
    },
    id: {
      type: String,
      required: true
    },
    date: {
      type: String,
      required: true
    }
  }
}
</script>

<style scoped>
.date{
  color: #82B1FF
}
</style>
