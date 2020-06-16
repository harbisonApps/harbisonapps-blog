<template>
  <div>
    <article class="p-2">
      <!-- eslint-disable-next-line vue/html-self-closing -->
      <v-divider class="my-2"></v-divider>
      <nuxt-link :to="'/blog/' + id" class="p-2 link-color">
        {{ title }}
      </nuxt-link>
    </article>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    id: {
      type: String,
      required: true
    }
  },
  asyncData (context) {
    return context.app.$storyapi.get('cdn/stories/', {
      version: context.isDev ? 'draft' : 'published',
      starts_with: 'blog/'
    })
      .then((res) => {
        return {
          // posts: res.data.stories.slice(0, 5).map((bp) => {
          posts: res.data.stories.map((bp) => {
            return {
              id: bp.slug,
              title: bp.content.title
            }
          })
        }
      })
  }
}
</script>

<style scoped>
 .link-color {
    color: #00695C;
    text-decoration-line: underline;
    font-size: 1.2rem;
  }
</style>
