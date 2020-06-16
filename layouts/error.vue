<template>
  <v-app dark class="m-4">
    <v-container>
      <v-card class="py-5">
        <div v-if="error.statusCode === 404" class="text-center">
          <h1 class="text-h5">
            {{ pageNotFound }}
          </h1>
        </div>
        <div v-else class="text-center">
          <h1 class="text-h3">
            {{ otherError }}
          </h1>
        </div>
        <div class="text-center">
          <NuxtLink exact class="link-color" to="/">
            <v-icon color="teal darken-4" x-large>
              mdi-home
            </v-icon>
            Home page
          </NuxtLink>
        </div>
      </v-card>
    </v-container>
  </v-app>
</template>

<script>
export default {
  layout: 'empty',
  props: {
    error: {
      type: Object,
      default: null
    }
  },
  head () {
    const title =
      this.error.statusCode === 404 ? this.pageNotFound : this.otherError
    return {
      title
    }
  },
  data () {
    return {
      pageNotFound: '404 Not Found',
      otherError: 'An error occurred'
    }
  }
}
</script>

<style scoped>
h1 {
  font-size: 20px;
}

.link-color {
    color: #00695C;
    text-decoration-line: underline;
    font-size: 1.2rem;
  }
</style>
