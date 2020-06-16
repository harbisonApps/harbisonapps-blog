<template>
  <div class="mb-4">
    <div class="masthead" role="img" aria-label="computer code">
      <h1 class="masthead-h1">
        {{ pageTitle }} Me
      </h1>
      <MastheadBtn
        to="services"
        text="[ services i provide ]"
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
import PostLinks from '~/components/Blog/PostLinks'
import ContactForm from '~/components/ContactForm'
import ServicesBtn from '~/components/Buttons/ServicesBtn'
import MastheadBtn from '~/components/Buttons/MastheadBtn'
export default {
  components: { PostLinks, ContactForm, ServicesBtn, MastheadBtn },
  data () {
    return {
      pageTitle: 'Contact',
      description: 'I would love to hear from you, let me know what you think of the site. Or if you are interested in working with me. Just fill out this form and I will get in touch with you as soon as possible.',
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'Your name is required',
        v => (v && v.length <= 20) || 'Name must be less than 20 characters'
      ],
      email: '',
      emailRules: [
        v => !!v || 'Please enter your e-mail',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
      ],
      select: null,
      items: [
        'Item 1',
        'Item 2',
        'Item 3',
        'Item 4'
      ]
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
  methods: {
    validate () {
      this.$refs.form.validate()
    },
    reset () {
      this.$refs.form.reset()
    },
    resetValidation () {
      this.$refs.form.resetValidation()
    }
  },
  head () {
    return {
      title: this.pageTitle + ' - Harbison Apps',
      meta: [
        // hid is used as unique identifier
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

.contact-form {
  width: 90%;
}
</style>
