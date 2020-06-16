<template>
  <div class=" mb-4">
    <div class="masthead" role="img" aria-label="computer code">
      <h1 class="masthead-h1">
        {{ pageTitle }}
      </h1>
      <MastheadBtn
        to="services"
        text="[ Services I Provide ]"
      />
    </div>
    <v-container>
      <v-layout
        column
        align-center
      >
        <v-flex>
          <v-sheet class="mt-2 px-1">
            <p class="text-center text-h6">
              {{ description }}
            </p>
            <v-row>
              <PostPreview
                v-for="post in posts"
                :id="post.id"
                :key="post.id"
                :title="post.title"
                :date="post.date"
                :excerpt="post.excerpt"
                :thumbnail="post.thumbnailUrl"
                class=""
              />
            </v-row>
          </v-sheet>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
import PostPreview from '@/components/Blog/PostPreview'
import MastheadBtn from '~/components/Buttons/MastheadBtn'
export default {
  components: {
    PostPreview, MastheadBtn
  },
  data () {
    return {
      pageTitle: 'In My Vue',
      description: 'A weekly blog dedicated to VueJs, the MEVN stack, and a handful of topics I find interesting.'
    }
  },
  asyncData (context) {
    return context.app.$storyapi.get('cdn/stories/', {
      version: context.isDev ? 'draft' : 'published',
      starts_with: 'blog/'
    })
      .then((res) => {
        return {
          posts: res.data.stories.map((bp) => {
            return {
              id: bp.slug,
              title: bp.content.title,
              excerpt: bp.content.excerpt,
              thumbnailUrl: bp.content.thumbnailUrl,
              date: bp.content.date
            }
          })
        }
      })
  },
  head () {
    return {
      title: this.pageTitle + ' - Harbison Apps',
      meta: [
        // hid is used as unique identifier.
        { hid: 'description', name: 'description', content: this.description }
      ]
    }
  }
}
</script>
<style scoped>

.masthead {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  text-align: center;
  width: 100%;
  height: 75vh;  /* if you don't want it to take up the full screen, reduce this number */
  background-size: cover;
  background-position: center;
  background: radial-gradient(ellipse at center, rgba(0,0,0,0) 0%, rgba(0,0,0,0) 0%, rgba(48,68,85,0.65) 100%),url(~static/laptop-code.jpg) no-repeat center center scroll;
}

.masthead-h1 {
  font-style: normal;
  font-weight: bold;
  color: #eee;
  font-size: 11vmin;
  letter-spacing: 0.03em;
  line-height: 1;
  text-shadow: 1px 2px 4px rgba(0, 0, 0, 0.8);
  margin-bottom: 68px;
}
</style>
