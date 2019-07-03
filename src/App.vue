<template lang="pug">
  div 
    div
      h1
        | Text Summarization
    div(id="app")
      Content
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "./components/HelloWorld.vue";
import Content from "./components/Content.vue";

@Component({
  components: {
    Content
  }
})
export default class App extends Vue {}
</script>

<style lang="sass">
body
  margin: 0
  padding: 0
#app
  font-family: "Avenir", Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px
</style>
