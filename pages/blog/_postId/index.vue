<template>
  <section id="blog-post" v-editable="blokPost">
    <div id="post-image" class="mx-auto text-center">
      <img :src="image" :alt="title" class="post-image">
    </div>
    <v-container>
      <v-card class="mt-n1">
        <article>
          <h1 id="post-title" class="text-center pt-2 h4">
            {{ title }}
          </h1>
          <p class="text-center my-n3">
            {{ date }}
          </p>
          <p class="text-center mt-n3">
            {{ excerpt }}
          </p>
          <p class="px-2 pb-4">
            {{ content }}
          </p>
        </article>
        <div class="text-center mt-2">
          <ServicesBtn />
        </div>
      </v-card>
    </v-container>
  </section>
</template>

<script>
import ServicesBtn from '~/components/Buttons/ServicesBtn'
export default {
  components: {
    ServicesBtn
  },
  asyncData (context) {
    return context.app.$storyapi.get('cdn/stories/blog/' + context.params.postId, {
      version: context.isDev ? 'draft' : 'published'
    }).then((res) => {
      return {
        blokPost: res.data.story.content,
        image: res.data.story.content.thumbnailUrl,
        title: res.data.story.content.title,
        date: res.data.story.content.date,
        excerpt: res.data.story.content.excerpt,
        content: res.data.story.content.content
      }
    })
  },
  head () {
    return {
      title: this.title + ' - In My Vue / Harbison Apps',
      meta: [
        // hid is used as unique identifier.
        { hid: 'description', name: 'description', content: this.excerpt },
        { hid: 'creationdate', name: 'creationdate', content: this.date },
        { hid: 'author', name: 'author', content: 'Brian Leabold, Harbison Apps' }
      ]
    }
  }
}
</script>

<style scoped>
#blog-post {
  margin: 0;
}

p {
  white-space: pre-line;
}

#post-image {
  /* align-content: center; */
  margin-top: 5px;
  background-color: #FAFAFA;
}
.post-image {
  max-width: 350px;
}

/* #post-image {
  z-index: 0;
} */
</style>
