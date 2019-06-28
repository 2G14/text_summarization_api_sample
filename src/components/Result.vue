<template lang="pug">
  div
    ul
      li(v-for="(item, index) in items" :key="index")
        | {{item.text}}
</template>

<script lang="ts">
import { Component, Prop, Emit, Watch, Vue } from "vue-property-decorator";

export default class Result extends Vue {
  @Prop()
  private items!: string[];
}
</script>

<style lang="sass" scoped>

</style>
