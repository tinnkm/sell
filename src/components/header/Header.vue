<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar" width="64" height="64">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name"> {{ seller.name }} </span>
        </div>
        <div class="description">
          {{ seller.description }}/{{ seller.deliveryTime }}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <!--<span class="icon" :class="classMap[seller.supports[0].type]"></span>-->
          <v-icon :type="seller.supports[0].type" :v-style="1"></v-icon>
          <span class="text">{{ seller.supports[0].description }}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="supports-count" @click="showDetail">
        <span class="count">{{ seller.supports.length }}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span><span class="bulletin-text">{{ seller.bulletin }}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background" >
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <transition name="fade">
      <div v-show="detailShow" class="detail">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <h1 class="name">{{ seller.name }}</h1>
          <div class="star-wrapper">
            <v-star :size="48" :score="seller.score" class=""></v-star>
          </div>
          <v-title :text="'优惠信息'">
            <ul v-if="seller.supports">
              <li class="support-item" v-for="(item, index) in seller.supports" :key="index">
                <!--<span class="icon" :class="classMap[item.type]"></span>-->
                <div class="icon-wrapper">
                  <v-icon :width="16" :height="16" :type="item.type" :v-style="2"></v-icon>
                </div>
                <span class="text">{{ item.description }}</span>
              </li>
            </ul>
          </v-title>
          <v-title :text="'商家信息'">
              <p class="text">{{ seller.bulletin }}</p>
          </v-title>
        </div>
      </div>
      <div class="detail-close" @click="hideDetail">
        <i class="icon-close"></i>
      </div>
    </div>
    </transition>
  </div>
</template>

<script>
import VStar from '@/components/star/Star'
import VTitle from '@/components/title/Title'
import VIcon from '@/components/icon/Icon'
export default {
  name: 'Header',
  props: {
    seller: {
      type: Object,
      default () {
        return {}
      }
    }
  },
  data () {
    return {
      detailShow: false
    }
  },
  methods: {
    showDetail () {
      this.detailShow = true
    },
    hideDetail () {
      this.detailShow = false
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  },
  components: {
    VStar,
    VTitle,
    VIcon
  }
}
</script>

<style lang="stylus" scoped>
@import "../../common/stylus/mixin.styl"

.header
  position relative
  color #fff
  overflow hidden
  background-color rgba(7,17,27,0.5)
  .content-wrapper
    padding 24px 12px 18px 24px
    position relative
    font-size 0px
    .avatar
      width 64px
      height 64px
      display inline-block
      vertical-align top
      img
        border-radius 2px
    .content
      margin-left 16px
      display inline-block
      .title
        margin 2px 0px 8px 0px
        .brand
          width 30px
          height 18px
          display inline-block
          bg-image('images/brand')
          background-size 30px 18px
          background-repeat no-repeat
          vertical-align top
        .name
          font-size 16px
          font-weight bold
          line-height 18px
          margin-left 6px
      .description
        font-size 12px
        line-height 12px
        margin-top 8px
      .support
        margin-top 10px
        margin-bottom 2px
        .text
          margin-left 4px
          line-height 12px
          font-size 10px
    .supports-count
      position absolute
      right 12px
      bottom 14px
      padding 0 8px
      height 24px
      line-height 24px
      border-radius 14px
      background-color rgba(0,0,0,0.2)
      text-align center
      .count
        vertical-align top
        font-size 10px
      .icon-keyboard_arrow_right
        margin-left 2px
        font-size 10px
        line-height 24px
  .bulletin-wrapper
    position relative
    height 28px
    line-height 28px
    /* 这里的22是由（（24+8）+ '>'图片的宽度）/2得到 */
    padding 0 22px 0 12px
    background-color rgba(7,17,27,.2)
    white-space: nowrap
    overflow hidden
    text-overflow: ellipsis
    .bulletin-title
      display: inline-block
      height 12px
      width 22px
      vertical-align top
      margin-top 8px
      bg-image('images/bulletin')
      background-size 22px 12px
      background-repeat no-repeat
    .bulletin-text
      margin 0 4px
      font-size 10px
    .icon-keyboard_arrow_right
      position absolute
      right 12px
      bottom 8px
      font-size 10px
  .background
    position absolute
    left 0
    top 0
    width 100%
    height 100%
    filter blur(10px)
    z-index -1
  .detail
    position fixed
    top 0
    left 0
    width 100%
    height 100%
    z-index 100
    overflow auto
    background-color rgba(7,17,27,0.8)
    backdrop-filter blur(10px)
    .detail-wrapper
      min-height 100%
      width 100%
      .detail-main
        margin-top 64px
        padding-bottom 64px
        .name
          height 16px
          line-height 16px
          font-size 16px
          font-weight 700
          text-align center
        .star-wrapper
          margin-top 16px
          line-height 24px
          width 100%
          text-align center
        .support-item
          padding 0 12px
          margin-bottom 12px
          font-size 0
          &:last-child
            margin-bottom 0
          .icon-wrapper
            display inline-block
            margin-right 6px
            vertical-align top
          .text
            line-height 16px
            font-size 12px
        .text
          padding 0 12px
          line-height 24px
          font-size 12px
    .detail-close
      position relative
      width 32px
      height 32px
      margin -64px auto 0 auto
      clear both
      font-size 32px
  .fade-enter-active
  .fade-leave-active
    transition all 0.5s ease
  .fade-enter-to
  .fade-leave
    opacity 1
    background-color rgba(7,17,27,0.8)
  .fade-enter
  .fade-leave-to
    opacity 0
    background-color rgba(7,17,27,0)
</style>
