<template>
  <nav
      color="cyan darken-4"
      flat
  >
    <v-snackbar v-model="snackbar" :timeout="4000" top color="success">
      <span>Awesome! You added a new project.</span>
      <v-btn color="white" flat @click="snackbar = false">Close</v-btn>
    </v-snackbar>

    <v-toolbar app>

      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>
        <span>ToDo List</span>
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <v-menu
          open-on-hover
          top
          offset-y
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn
              color="primary"
              dark
              v-bind="attrs"
              v-on="on"
          >
            Shortcuts
          </v-btn>
        </template>

        <v-list>
          <v-list-item
              v-for="link in links" :key="link.text"  router :to="link.route"
          >
            <v-list-item-title>{{ link.text }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>

      <v-btn
          class="ma-2"
          color="red"
          dark
      >
        Sign Out
        <v-icon
            dark
            right
        >
          mdi-cancel
        </v-icon>
      </v-btn>
    </v-toolbar>
    <v-navigation-drawer v-model="drawer"  app class="red darken-4">
      <v-layout column align-center>
        <v-flex class="mt-5">
          <v-avatar size="100">
            <img src="/iul.png">
          </v-avatar>
          <p class="blue--text mt-1 title font-weight-bold">Iulian Patrunjel</p>
        </v-flex>
        <v-flex class="mt-4 mb-3">
          <Popup @projectAdded="snackbar = true" />
        </v-flex>
      </v-layout>

      <v-list-item v-for="link in links" :key="link.text"  router :to="link.route">
        <v-list-item-title class="title">{{ link.icon }} {{ link.text }}</v-list-item-title>
      </v-list-item>
    </v-navigation-drawer>


  </nav>
</template>


<script>

import Popup from './Popup'
export default {
  components: { Popup },
 data() {
   return {
     drawer : false,
     links: [
       { icon: 'mdi-home', text: 'Dashboard' , route: '/'},
       { icon: 'mdi-folder', text: 'My Projects' , route: '/projects'},
       { icon: 'mdi-face', text: 'Team' , route: '/team'},
     ],
     snackbar: false
   }
 }
}
</script>