<template lang="pug">
  div(class="textarea")
    div(class="label")
      label(:for="label")
        | {{label}}
    textarea(:name="label" v-model="text" @change="updateValue" :placeholder="placeholder" :maxlength="maxlength")
</template>

<script lang="ts">
import { Component, Prop, Emit, Watch, Vue } from "vue-property-decorator";

@Component
export default class Textarea extends Vue {
  @Prop({ type: String })
  private label?: string;
  @Prop({
    type: String,
    required: true,
    default: ""
  })
  private value!: string;
  @Prop({ type: String })
  private placeholder?: string;
  @Prop({ type: Number })
  private maxlength?: number;

  private text: string = this.value;
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