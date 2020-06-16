<template>
  <div class="mb-4">
    <div class="masthead" role="img" aria-label="computer code">
      <h1 class="masthead-h1">
        {{ pageTitle }}
      </h1>
      <MastheadBtn
        to="services"
        text="[ Services I Provide ]"
      />
    </div>
    <!-- <v-layout
      column
      align-center
    >
      <v-flex> -->
    <v-container>
      <v-sheet class="mt-2 mx-2">
        <!-- <v-card-text> -->
        <v-row
          align="center"
          justify="center"
        >
          <v-col
            cols="12"
            sm="9"
            md="9"
          >
            <p class="mb-2 text-center">
              Pride, Professionalism, Attention to Detail
            </p>
            <h2 class="text-center text-h5 mt-2">
              Why Do I Love Using Vue?
            </h2>
            <p class="pa-2 mt-2">
              Because Vue has learned form the other JavaScript frameworks on the market. Implementing
              their best parts and yet remaining as unopinionated as possible. Vue also comes in a variety
              of flavors.
            </p>
            <div class="text-xs-right">
              <em><small>&mdash; Brian Leabold</small></em>
            </div>
            <hr class="my-3">
            <!-- <a
              href="https://nuxtjs.org/"
              target="_blank"
            >
              Nuxt Documentation
            </a> -->
            <br>
            <!-- <a
              href="https://github.com/nuxt/nuxt.js"
              target="_blank"
            >
              Nuxt GitHub
            </a> -->
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

        <!-- <p>
              For more information on Vuetify, check out the <a
                href="https://vuetifyjs.com"
                target="_blank"
              >
                documentation
              </a>.
            </p>
            <p>
              If you have questions, please join the official <a
                href="https://chat.vuetifyjs.com/"
                target="_blank"
                title="chat"
              >
                discord
              </a>.
            </p>
            <p>
              Find a bug? Report it on the github <a
                href="https://github.com/vuetifyjs/vuetify/issues"
                target="_blank"
                title="contribute"
              >
                issue board
              </a>.
            </p> -->
        <!-- </v-card-text>
        <v-card-actions class="text-center"> -->
        <!-- <v-spacer /> -->
        <v-btn
          color="primary"
          nuxt
          to="/inspire"
        >
          Continue
        </v-btn>
        <!-- </v-card-actions> -->
      </v-sheet>
    </v-container>
    <!-- </v-flex>
    </v-layout> -->
  </div>
</template>

<script>
// import Logo from '~/components/Logo.vue'
// import VuetifyLogo from '~/components/VuetifyLogo.vue'
import MastheadBtn from '~/components/Buttons/MastheadBtn'
import PostLinks from '~/components/Blog/PostLinks'
export default {
  components: { PostLinks, MastheadBtn
    // Logo,
    // VuetifyLogo
  },
  data () {
    return {
      pageTitle: 'Welcome'
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
        { hid: 'description', name: 'description', content: 'My custom description' }
      ]
    }
  }

}
</script>

<style scoped>
.border {
  border: black solid 1px;
}

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
