<template>
  <div class="title-wrapper">
    <div class="title">
      <div class="line"></div>
      <div class="text">{{ text }}</div>
      <div class="line"></div>
    </div>
    <!-- 用户输入内容 -->
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      default () {
        return '标题'
      }
    }
  },
  name: 'Title'
}
</script>

<style lang="stylus" scoped>
  .title-wrapper
    width 80%
    margin 0 auto
    .title
      display flex
      margin 28px auto 24px auto
      .line
        position relative
        top -6px
        flex 1
        border-bottom 1px solid rgba(255,255,255,0.2)
      .text
        padding 0 12px
        font-size 14px
        font-weight 700
</style>
