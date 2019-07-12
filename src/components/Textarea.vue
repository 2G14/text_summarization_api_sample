<template lang="pug">
  div.textarea
    div.label
      label(:for="label")
        | {{label}}
    textarea(:id="label" v-model="text" @change="updateValue" :placeholder="placeholder" :maxlength="maxlength")
</template>

<script lang="ts">
import { Component, Prop, Emit, Vue } from "vue-property-decorator";

@Component
export default class Textarea extends Vue {
  /**
   * label
   */
  @Prop({ type: String })
  private label?: string;
  /**
   * initial value
   */
  @Prop({
    type: String,
    required: true,
    default: ""
  })
  private value!: string;
  /**
   * placeholder
   */
  @Prop({ type: String })
  private placeholder?: string;
  /**
   * maxlength
   */
  @Prop({ type: Number })
  private maxlength?: number;
  /**
   * text
   */
  private text: string = this.value;
  /**
   * emit input
   */
  @Emit("input")
  private input(value: string) {}
  /**
   * emit change
   */
  @Emit("change")
  private change() {}
  /**
   * onchange func
   */
  private updateValue() {
    this.input(this.text);
    this.change();
  }
}
</script>

<style lang="sass" scoped>
$blue: #528fcc
$pink: #ff99d6

div.textarea
  div.label
    label
  textarea
    border: 3px solid $pink
    border-radius: 0.67em
    padding: 0.5em
    background-color: snow
    width: 80vw
    height: 20vh
    font-size: 1em
    line-height: 1.2
    outline: none
</style>