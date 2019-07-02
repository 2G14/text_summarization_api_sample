<template lang="pug">
  div(class="select")
    div(class="label")
      label(:for="label")
        | {{label}}
    select(:name="label" v-model="selected" @change="updateValue")
      template(v-for="(option, index) in options")
        option(:value="option.value" :key="index")
          | {{ option.label }}
</template>

<script lang="ts">
import { Component, Prop, Emit, Watch, Vue } from "vue-property-decorator";

@Component
export default class Select extends Vue {
  @Prop()
  private label!: string | number;
  @Prop()
  private value!: string | number;
  @Prop()
  private options!: Array<{ label: string | number; value: string | number }>;

  private selected: string | number = this.value;

  private mounted(): void {
    this.$emit("input", this.options[0].value);
  }
  private updateValue() {
    this.$emit("input", this.selected);
    this.$emit("change");
  }
}
</script>

<style lang="sass" scoped>
$input-color: blue;

div.select
  width: 200px
  margin: auto
  padding: auto
  position: relative
  border: 1px solid #bbbbbb
  border-radius: 2px
  background: #ffffff
  &::before
    content: ''
    position: absolute
    top: 0.8em
    right: 0.9em
    width: 0
    height: 0
    padding: 0
    border-left: 6px solid transparent
    border-right: 6px solid transparent
    border-top: 6px solid #666666
    pointer-events: none
  div.label
    label
  select
    text-align: center
    width: 100%
    cursor: pointer
    text-overflow: ellipsis
    border: none
    outline: none
    background: transparent
    background-image: none
    box-shadow: none
    appearance: none
    padding: 8px 38px 8px 8px
    color: #666666
    &::-ms-expand
      display: none
    option
</style>
