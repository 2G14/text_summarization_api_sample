<template lang="pug">
  div.loading(v-show="show")
    div.overlay
      div(v-text="text")
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Loading extends Vue {
  /**
   * 表示中か否か
   */
  @Prop({ type: Boolean, required: true, default: false })
  private show!: boolean;
  /**
   * テキスト
   */
  @Prop({ type: String })
  private text?: string;
}
</script>

<style lang="sass" scoped>
div.loading
  div.overlay
    /* 少し暗く */
    background-color: rgba(0, 0, 0, 0.75)
    /* 画面全体に広げる */
    position: absolute
    height: 100vh
    width: 100vw
    left: 0
    top: 0
    /* 子要素を上下左右中央寄せ */
    display: flex
    align-items: center
    justify-content: center
    div
      color: #fff
      animation-name: blink
      animation-duration: 600ms
      animation-timing-function: ease-in-out
      animation-direction: alternate
      animation-iteration-count: infinite

@keyframes blink
  from
    opacity: 0
  to
    opacity: 1
</style>
