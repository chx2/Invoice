<template>
  <b-container id="app">
    <home v-if="!start" @create="fromNew" @file-loaded="fromFile"></home>
    <div v-else>
      <div v-if="!loading">
        <setup @submit="toNew" v-if="!data"></setup>
        <invoice :data="data" v-else></invoice>
      </div>
      <load v-else></load>
    </div>
  </b-container>
</template>

<script>
import Home from "@/components/Home";
import Setup from "@/components/Setup";
import Load from "@/components/Load";
import Invoice from "@/components/Invoice";
export default {
  name: 'App',
  components: {Invoice, Load, Setup, Home},
  data() {
    return {
      loading: false,
      start: false,
      data: null
    }
  },
  methods: {
    fromNew() {
      this.start = true
    },
    fromFile(json) {
      this.data = json
      this.start = true
      this.loading = true
      let self = this
      window.setTimeout(function(){
        self.loading = false
      }, 3000)
    },
    toNew(data) {
      this.data = data
      this.loading = true
      let self = this
      window.setTimeout(function(){
        self.loading = false
      }, 3000)
    }
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
