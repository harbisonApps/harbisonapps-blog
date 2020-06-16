<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
      dark
      class="dark"
    >
      <v-list shaped>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" color="primary" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" name="menu" aria-label="menu" color="white" />
      <v-spacer />
      <v-toolbar-title v-text="title" class="text-h4 white--text" />
      <v-spacer />
    </v-app-bar>
    <v-main>
      <nuxt />
    </v-main>
    <v-footer>
      <v-spacer />
      <img class="footer-image" src="../static/nuxt_logo.png" alt="Nuxt" title="Nuxt">
      <span class="mx-2">&copy; 2019 Harbison Apps</span>
      <img class="footer-image" src="data:image/png;base64,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" alt="Nuxt" title="Nuxt">
      <v-spacer />
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-home',
          title: 'Home',
          to: '/'
        },
        {
          icon: 'mdi-format-list-bulleted-type',
          title: 'Services',
          to: '/services'
        },
        {
          icon: 'mdi-newspaper-variant-outline',
          title: 'In My Vue',
          to: '/blog'
        },
        {
          icon: 'mdi-email-outline',
          title: 'Contact',
          to: '/contact'
        }
      ],
      miniVariant: false,
      // right: true,
      // rightDrawer: false,
      title: 'Harbison Apps'
    }
  }
}
</script>

<style scoped>
p {
  font-size: 1.1rem;
}
.footer-image {
   height: 50px;
 }
</style>
