<template lang="pug">
  div(class="textarea")
    div(class="label")
      label(:for="label")
        | {{label}}
    textarea(:id="label" v-model="text" @change="updateValue" :placeholder="placeholder" :maxlength="maxlength")
</template>

<script lang="ts">
import { Component, Prop, Emit, Watch, Vue } from "vue-property-decorator";

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
   * onchange func
   */
  private updateValue() {
    this.$emit("input", this.text);
    this.$emit("change");
  }
}
</script>

<style lang="sass" scoped>
div.textarea
  div.label
    label
  textarea
    border: 3px solid #ff99d6
    border-radius: 0.67em
    padding: 0.5em
    background-color: snow
    width: 30em
    height: 140px
    font-size: 1em
    line-height: 1.2
    outline: none
</style>