<template lang="pug">
  div(class="list")
    div(class="label")
      label(:for="label")
        | {{label}}
    ul(:name="label")
      template(v-for="(item, index) in items")
        li(:key="index")
          div()
            | {{item}}
</template>

<script lang="ts">
import { Component, Prop, Emit, Watch, Vue } from "vue-property-decorator";

@Component
export default class List extends Vue {
  /** prop */
  @Prop({ type: String })
  private label?: string;
  @Prop({ type: Array, required: true, default: [] })
  private items!: string[];
}
</script>

<style lang="sass" scoped>
div.list
  div.label
    label
  ul
    padding: 0
    list-style: none
    li
      div
</style>
