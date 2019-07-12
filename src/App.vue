<template lang="pug">
  div 
    div
      h1
        | Text Summarization
    div#app
      Content
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Content from "@/components/Content.vue";

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
  background: #2e8b57
  text-align: center
  h1
</style>
