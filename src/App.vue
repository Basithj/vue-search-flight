<template>
  <div id="app">
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <SearchFlight/>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import SearchFlight from './components/SearchFlight.vue'

export default {
  name: 'App',
  props:{

  },
  components: {
    SearchFlight
  },
  mounted: function() {
      
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
