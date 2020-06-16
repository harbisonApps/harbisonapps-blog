<template>
  <div class="mb-4">
    <div class="masthead" role="img" aria-label="computer code">
      <h1 class="masthead-h1">
        {{ pageTitle }}
      </h1>
      <MastheadBtn
        to="blog"
        text="[ In My Vue ]"
      />
    </div>
    <v-container>
      <v-sheet class="mt-2 mx-2">
        <v-row>
          <v-col
            cols="12"
            sm="9"
            md="9"
          >
            <p>
              {{ description }}
            </p>
            <ContactForm />

            <ServicesBtn />
            <!-- </v-row> -->
          </v-col>
          <v-col cols="12" sm="3" md="3">
            <v-card rounded class="pa-2">
              <h2 class="text-center">
                In My Vue
              </h2>
              <PostLinks
                v-for="post in posts"
                :id="post.id"
                :key="post.id"
                :title="post.title"
              />
            </v-card>
          </v-col>
        </v-row>
      </v-sheet>
    </v-container>
  </div>
</template>

<script>
import MastheadBtn from '~/components/Buttons/MastheadBtn'
import PostLinks from '~/components/Blog/PostLinks'
export default {
  components: {
    MastheadBtn, PostLinks
  },
  data () {
    return {
      pageTitle: 'Services',
      description: 'From dynamic web apps and static sites, to adding features to your website; I will give you what you need to improve your web presence.'
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
