<template lang="pug">
  div(class="list")
    div(class="label")
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
  width: 200px
  margin: 5px auto
  padding: auto
  position: relative
  div.label
    label
  ul
    padding: 0
    list-style: none
    li
      div
        border: solid 1px black
        border-radius: 2px
</style>
