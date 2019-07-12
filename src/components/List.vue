<template lang="pug">
  div.list
    div.label
      label(:for="label")
        | {{label}}
    ul(:id="label")
      template(v-for="(item, index) in items")
        li(:key="index")
          div(class="item")
            | {{item}}
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class List extends Vue {
  /**
   * label
   */
  @Prop({ type: String })
  private label?: string;
  /**
   * list items
   */
  @Prop({ type: Array, required: true, default: [] })
  private items!: string[];
}
</script>

<style lang="sass" scoped>
$blue: #528fcc
$lightblue: #99ccff
$pink: #ff99d6
$lightpink: #ffb3e0

div.list
  width: 80vw
  margin: 5px auto
  padding: 0
  position: relative
  border: solid 1px black
  div.label
    label
  ul
    margin: 0
    padding: 0
    list-style: none
    border-top: solid 1px $pink
    border-bottom: solid 1px $pink
    li
      div
        padding: 0.5em
        line-height: 1.5
        border-top: solid 1px $pink
        border-bottom: solid 1px $pink
        border-left: solid 2px $pink
        border-right: solid 2px $pink
        background: $lightpink
</style>
