<template lang="pug">
  div(class="select")
    div(class="label")
      label(:for="label")
        | {{label}}
    select(:name="label" v-model="selected" v-on:change="updateValue")
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
  }
}
</script>

<style lang="sass" scoped>
div.select
  div.label
    label
  select
    option
</style>
