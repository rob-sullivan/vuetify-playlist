<template>
    <nav>
        <v-app-bar app flat>
            <v-app-bar-nav-icon class="grey--text" @click="drawer = !drawer"></v-app-bar-nav-icon>
            <v-toolbar-title class="text-uppercase grey--text">
                <span class="font-weight-light">Todo</span>
                <span>Ninja</span>
            </v-toolbar-title>
            <v-spacer></v-spacer>
            <!-- dropdown menu -->
              <div class="text-center">
                <v-menu offset-y>
                  <template v-slot:activator="{ on, attrs }">
                    <v-btn
                      text
                      color="grey"
                      dark
                      v-bind="attrs"
                      v-on="on"
                    >
                      <v-icon left>mdi-arrow-down-drop-circle-outline</v-icon>
                      <span>Menu</span>
                    </v-btn>
                  </template>
                  <v-list>
                    <v-list-item v-for="link in links" :key="link.text" router :to="link.route" color="primary">
                      <v-list-item-title>{{ link.text }}</v-list-item-title>
                    </v-list-item>
                  </v-list>
                </v-menu>
              </div>
            <v-btn color="grey" text>
                <span>Sign Out</span>
                <v-icon right>mdi-exit-to-app</v-icon>
            </v-btn>
        </v-app-bar>
        <v-navigation-drawer app v-model="drawer" class="primary">
          <v-layout column align-center>
            <v-flex class="mt-5">
              <v-avater size="100">
                <img src="/avatar-1.png" alt="">
              </v-avater>
              <p class="white--text subheading mt-1">The Net Ninja</p>
            </v-flex>
            <v-flex mt-4 mb-3>
              <Popup />
            </v-flex>
          </v-layout>
        <v-list>
            <v-list-item v-for="link in links" :key="link.text" router :to="link.route">
            <v-list-item-action>
                <v-icon class="white--text">{{ link.icon }}</v-icon>
            </v-list-item-action>
            <v-list-item-content>
                <v-list-item-title class="white--text">{{ link.text }}</v-list-item-title>
            </v-list-item-content>
            </v-list-item>
        </v-list>
        </v-navigation-drawer>
    </nav>
</template>
<script>
import Popup from './Popup'
export default {
  components: {Popup},
  data() {
    return {
      drawer: false,
      links: [
        { icon: 'mdi-view-dashboard', text: 'Dashboard', route: '/' },
        { icon: 'mdi-folder', text: 'My Projects', route: '/projects' },
        { icon: 'mdi-account', text: 'Team', route: '/team' },
      ]
    }
  }
}
</script>