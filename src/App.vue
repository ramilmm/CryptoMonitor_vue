<template>
    <router-view></router-view>
</template>

<script>
import Dashboard from './components/Dashboard'
import HitBTC from './components/charts/HitBTC.vue'
import Poloniex from './components/charts/Poloniex.vue'
import TableComponent from './components/TableComponent.vue'

export default {
  name: 'app',
  components: {
    Dashboard, HitBTC, Poloniex, TableComponent
  }
}
</script>

<style>
</style>
