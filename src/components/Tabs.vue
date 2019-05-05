<template>
  <v-tabs v-model="active">
    <v-tab v-for="(title, index) in titles" :key="index" ripple>
      {{title}}
    </v-tab>
    <v-tab-item v-for="(title, index) in titles" :key="index">
      <AssetHealth v-if="index === 1"/>
      <EmptyTab v-else/>
    </v-tab-item>
  </v-tabs>
</template>

<script>
import EmptyTab from './EmptyTab.vue'
import AssetHealth from './AssetHealth.vue'
export default {
  data: () => ({
    active: 1,
    titles: [
      'dashboard',
      'asset health',
      'work orders'
    ]
  }),
  components: {
    EmptyTab,
    AssetHealth
  }
}
</script>

<style>
  .v-tabs__item--active {
    color: #1976d2
  }
</style>

