<template>
  <v-container>
    <v-card class="card--flex-toolbar" tile>
      <v-toolbar card prominent dense class="blue white--text">
        <v-toolbar-title class="body-2">
          Asset overview
        </v-toolbar-title>
        <v-icon class="white--text inline-icon">arrow_forward</v-icon>
        <div class="circle"></div>
        <div class="body-2">Master station 1-1</div>

        <v-spacer></v-spacer>

        <v-btn icon>
          <v-icon class="white--text">place</v-icon>
        </v-btn>
      </v-toolbar>

      <v-divider></v-divider>

      <v-card-text>
        <v-tabs v-model="activeTab">
          <v-tab v-for="(title, index) in tabTitles" :key="index" ripple>
            {{title}}
          </v-tab>
          <v-tab-item v-for="(title, index) in tabTitles" :key="index">
            <TorqueProfile v-if="index === 3"/>
            <EmptyTab v-else/>
          </v-tab-item>
        </v-tabs>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
import EmptyTab from './EmptyTab.vue'
import TorqueProfile from './TorqueProfile.vue'

export default {
  data: () => ({
    activeTab: 3,
    tabTitles: [
      'events',
      'position',
      'travel time',
      'torque profile',
      'work orders',
      'alarms analytics'
    ]
  }),
  components: {
    EmptyTab,
    TorqueProfile
  }
}
</script>


<style>
  .inline-icon {
    padding: 0 0.6em;
  }
  .circle {
    background-color: #ef5350;
    height: 17px;
    width: 17px;
    border-radius: 50%;
    border-style: solid;
    border-width: 2px;
    border-color: white;
    margin-right: 0.6em;
  }
  .v-card__text {
    padding: 0;
  }
</style>

