<template lang="pug">
  div(class="button")
    div(class="label")
      label(:for="label")
        | {{label}}
    button(type="button" @click="click")
      | {{text}}
</template>

<script lang="ts">
import { Component, Prop, Emit, Watch, Vue } from "vue-property-decorator";

@Component
export default class Button extends Vue {
  @Prop({ type: String })
  private label?: string;
  @Prop({ type: String, required: true, default: "" })
  private text!: string;
  private click(): void {
    this.$emit("click");
  }
}
</script>

<style lang="sass" scoped>
div.button
  width: 200px
  margin: 5px auto
  padding: auto
  position: relative
  div.label
    label
  button
    display: inline-block
    padding: 0.5em 1em
    text-decoration: none
    background: #ff99d6
    color: black
    border: solid 1px black
    border-bottom: solid 2px black
    border-radius: 3px
    outline: none
  button:active
    transform: translateY(1px)
    border-bottom: solid 1px black
</style>
