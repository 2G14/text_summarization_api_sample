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
import { Component, Prop, Emit, Watch, Vue } from "vue-property-decorator";

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
    border-top: solid 1px #af3dcc
    border-bottom: solid 1px #af3dcc
    li
      div
        padding: 0.5em
        line-height: 1.5
        border-top: solid 1px #af3dcc
        border-bottom: solid 1px #af3dcc
        border-left: solid 2px #af3dcc
        border-right: solid 2px #af3dcc
        background: #ffb3e0
</style>
