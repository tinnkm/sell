<template>
<div class="star" :class="starType">
  <span v-for="(item, index) in classItem" :key="index" class="star-item" :class="item"></span>
</div>
</template>

<script>
const CLS_ON = 'on'
const CLS_OFF = 'off'
const CLS_HALF = 'half'
export default {
  props: {
    size: {
      type: Number,
      default () {
        return 32
      }
    },
    score: {
      type: Number,
      default () {
        return 0
      }
    },
    length: {
      type: Number,
      default () {
        return 5
      }
    }
  },
  name: 'Star',
  computed: {
    starType () {
      return 'star-' + this.size
    },
    classItem () {
      let result = []
      let hasDecimal = false
      let intValue = Math.round(this.score)
      if (this.score > intValue) {
        hasDecimal = true
      }
      for (let i = 0; i < intValue; i++) {
        result.push(CLS_ON)
      }
      if (hasDecimal) {
        result.push(CLS_HALF)
      }
      while (result.length < this.length) {
        result.push(CLS_OFF)
      }
      return result
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import "../../common/stylus/mixin.styl"
.star
  font-size 0
  .star-item
    display inline-block
    background-repeat no-repeat
    &:last-child
      margin-right 0
&.star-48
  .star-item
    width 20px
    height 20px
    background-size 20px 20px
    margin-right 22px
    &.on
      bg-image('images/star48_on')
    &.off
      bg-image('images/star48_off')
    &.half
      bg-image('images/star48_half')
&.star-36
  .star-item
    width 15px
    height 15px
    background-size 15px 15px
    margin-right 6px
    &.on
      bg-image('images/star36_on')
    &.off
      bg-image('images/star36_off')
    &.half
      bg-image('images/star36_half')
&.star-24
  .star-item
    width 10px
    height 10px
    background-size 10px 10px
    margin-right 3px
    &.on
      bg-image('images/star24_on')
    &.off
      bg-image('images/star24_off')
    &.half
      bg-image('images/star24_half')
</style>
