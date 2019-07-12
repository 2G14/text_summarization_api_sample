<template lang="pug">
  div.select
    div.label
      label(:for="label")
        | {{label}}
    select(:id="label" v-model="selected" @change="updateValue")
      template(v-for="(option, index) in options")
        option(:value="option.value" :key="index")
          | {{ option.label }}
</template>

<script lang="ts">
import { Component, Prop, Emit, Watch, Vue } from "vue-property-decorator";

@Component
export default class Select extends Vue {
  /**
   * label
   */
  @Prop({ type: String })
  private label?: string;
  /**
   * initial value
   */
  @Prop({
    type: [String, Number],
    required: true,
    default: ""
  })
  private value!: string | number;
  /**
   * options
   */
  @Prop({ type: Array, required: true, default: [] })
  private options!: Array<{ label: string | number; value: string | number }>;
  /**
   * selected option
   */
  private selected: string | number = this.value;
  /**
   * updated
   */
  private updated() {
    this.selected = this.value;
  }
  /**
   * onchange func
   */
  private updateValue() {
    this.$emit("input", this.selected);
    this.$emit("change");
  }
}
</script>

<style lang="sass" scoped>
div.select
  width: 200px
  margin: 5px auto
  padding: auto
  position: relative
  border: solid 1px black
  border-radius: 2px
  background: #ff99d6
  color: black
  div.label
    label
  select
    text-align: center
    width: 100%
    cursor: pointer
    text-overflow: ellipsis
    font-size: 16px
    border: none
    border-top: solid 1px black
    border-radius: 0
    outline: none
    background: #ffb3e0
    background-image: none
    box-shadow: none
    appearance: none
    padding: 8px 38px 8px 8px
    &::-ms-expand
      display: none
    option
</style>
