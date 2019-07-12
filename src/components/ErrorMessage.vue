<template lang="pug">
  div.error_message(v-show="existsError")
    div.message
      | {{ message }}
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class ErrorMessage extends Vue {
  /**
   * error message
   */
  @Prop({ type: String, required: true, default: "error" })
  private message!: string;
  /**
   * error exists
   */
  @Prop({ type: Boolean, required: true, default: false })
  private existsError!: boolean;
}
</script>

<style lang="sass" scoped>
div.error_message
  div.message
    background: rgba(255, 0, 0, 0.35)
    font-weight: bold
    color: #b3122d
    white-space: pre-wrap
</style>
