<template>
  <v-app>
    <v-toolbar app clipped-left dense flat>
      <v-toolbar-title class="headline text-uppercase">
        <span class="font-weight-light">predictable maintenance</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <v-menu :nudge-width="100">
          <template v-slot:activator="{ on }">
            <v-btn v-on="on" flat>
              <span>Juan Felipe Balcero</span>
              <v-icon>arrow_drop_down</v-icon>
            </v-btn>
          </template>

          <v-list>
            <v-list-tile
              v-for="item in userMenu"
              :key="item"
            >
              <v-list-tile-title v-text="item"></v-list-tile-title>
            </v-list-tile>
          </v-list>
        </v-menu>
        <v-btn flat href="#" target="_blank">
          <v-icon>power_settings_new</v-icon>
        </v-btn>
      </v-toolbar-items>
    </v-toolbar>

    <v-navigation-drawer fixed app clipped>
      <v-toolbar card prominent dense class="blue white--text">
        <v-icon class="white--text">arrow_back</v-icon>
        <v-toolbar-title class="toolbar__title">
          Terminal overview
        </v-toolbar-title>

        <v-spacer></v-spacer>

        <v-btn icon>
          <v-icon class="white--text">menu</v-icon>
        </v-btn>
      </v-toolbar>

      <img src="./assets/images/port.jpg"/>

      <v-list class="pt-0">
        <v-list-tile v-for="item in items" :key="item.title">
          <v-list-tile-content>
            <v-list-tile-sub-title>{{ item.label }}</v-list-tile-sub-title>
            <v-list-tile-title>{{ item.title }}</v-list-tile-title>
          </v-list-tile-content>
          <v-list-tile-action v-if="item.icon">
            <v-icon class="blue--text">{{ item.icon }}</v-icon>
          </v-list-tile-action>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>

    <v-content>
      <Tabs/>
    </v-content>
  </v-app>
</template>

<script>
import Tabs from './components/Tabs'

export default {
  name: 'App',
  components: {
    Tabs
  },
  data () {
    return {
      items: [
        { title: 'WEST', label: 'Terminal name' },
        { title: 'NLD', label: 'Country code' },
        { title: '3198 LK EUROPOORT', icon: 'place', label: 'Address' },
      ],
      right: null,
      userMenu: [
        'Account',
        'Settings',
        'Log out'
      ]
    }
  }
}
</script>

<style>
  .toolbar__title {
    text-transform: uppercase;
    font-size: 14px;
    font-weight: 500;
    line-height: normal;
  }
  img {
    width: 100%;
  }
  .v-list {
    margin-top: 1.563em;
  }
  .v-list__tile {
    padding: 0.5em;
  }
  .v-list__tile__content {
    margin-left: 1.4em;
  }
  .v-list__tile__title {
    font-size: 1.2em;
  }
</style>
