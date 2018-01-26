<template>
  <span class="icon" :class="subClass" :style="styleObj" ></span>
</template>

<script>
export default {
  name: 'icon',
  props: {
    width: {
      type: Number,
      default () {
        return 12
      }
    },
    height: {
      type: Number,
      default () {
        return 12
      }
    },
    type: {
      type: Number,
      default () {
        return 1
      }
    },
    VStyle: {
      type: Number,
      default () {
        return 1
      }
    }
  },
  computed: {
    subClass () {
      let classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
      return [classMap[this.type], 'style' + this.VStyle]
    },
    styleObj () {
      return {
        width: this.width + 'px',
        height: this.height + 'px',
        backgroundSize: this.width + 'px' + ' ' + this.height + 'px'
      }
    }
  },
  created () {

  }
}
</script>

<style lang="stylus" scoped>
  @import "../../common/stylus/mixin.styl"
.icon
  vertical-align top
  display inline-block
  background-repeat no-repeat
  &.decrease
    &.style1
      bg-image("images/decrease_1")
    &.style2
      bg-image("images/decrease_2")
    &.style3
      bg-image("images/decrease_3")
    &.style4
      bg-image("images/decrease_4")
  &.discount
    &.style1
      bg-image("images/discount_1")
    &.style2
      bg-image("images/discount_2")
    &.style3
      bg-image("images/discount_3")
    &.style4
      bg-image("images/discount_4")
  &.guarantee
    &.style1
      bg-image("images/guarantee_1")
    &.style2
      bg-image("images/guarantee_2")
    &.style3
      bg-image("images/guarantee_3")
    &.style4
      bg-image("images/guarantee_4")
  &.invoice
    &.style1
      bg-image("images/invoice_1")
    &.style2
      bg-image("images/invoice_2")
    &.style3
      bg-image("images/invoice_3")
    &.style4
      bg-image("images/invoice_4")
  &.special
    &.style1
      bg-image("images/special_1")
    &.style2
      bg-image("images/special_2")
    &.style3
      bg-image("images/special_3")
    &.style4
      bg-image("images/special_4")
</style>
