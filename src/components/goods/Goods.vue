<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul v-if="goods">
        <li v-for="(item, index) in goods" :key="index" class="menu-item">
          <span class="text">
            <div v-show="item.type > 0" class="icon-wrapper">
              <v-icon class="icon-wrapper" :type="item.type" :width="12" :height="12" :v-style="3"></v-icon>
            </div>{{ item.name }}</span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper">
      <ul>
        <li v-for="(item,index) in goods" class="food-list" :key="index">
          <h1 class="title">{{ item.name }}</h1>
          <ul>
            <li v-for="(food,i) in item.foods" class="food-item" :key="i">
              <div class="icon">
                <img width="57" height="57" :src="food.icon" alt="">
              </div>
              <div class="content">
                <h2 class="name">{{ food.name }}</h2>
                <p class="desc">{{ food.description }}</p>
                <div class="extra">
                  <span class="count">月售{{ food.sellCount }}份</span><span>好评率{{ food.rating }}%</span>
                </div>
                <div class="price">
                  <span class="now">￥{{ food.price }}</span>
                  <span class="old" v-show="food.oldPrice">￥{{ food.oldPrice }}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import VIcon from '@/components/icon/Icon'
const ERR_OK = 0
export default {
  name: 'Goods',
  data () {
    return {
      goods: []
    }
  },
  components: {
    VIcon
  },
  created () {
    this.$http.get('api/goods').then(
      (res) => {
        let data = res.body
        if (data.errno === ERR_OK) {
          this.goods = data.data
        }
      }
    )
  }
}
</script>

<style lang="stylus" scoped>
  @import "../../common/stylus/mixin.styl"
  @import "../../common/stylus/base.styl"
.goods
  display flex
  position absolute
  top 174px
  bottom 46px
  width 100%
  overflow hidden
  .menu-wrapper
    flex 0 0 80px
    width 80px
    background-color #f3f5f7
    .menu-item
      display table
      height 50px
      width 56px
      line-height 14px
      margin 0 auto
      font-size 0
      .text
        display table-cell
        width 56px
        vertical-align middle
        border-1px(rgba(7,17,27,0.1))
        font-size 12px
        .icon-wrapper
          display inline-block
          margin-right 2px
  .foods-wrapper
    flex 1
    .title
      padding-left 14px
      height 26px
      line-height 26px
      font-size 12px
      color rgb(147,153,159)
      background-color #f3f5f7
      border-left 2px solid #d9dde1
    .food-item
      display flex
      margin 18px
      padding-bottom 18px
      border-1px(rgba(7,17,27,0.1))
      &:last-child
        border-1px(rgba(7,17,27,0.1),false)
        margin-bottom 0
      .icon
        flex 0 0 57px
        margin-right 10px
        border-radius 1px
      .content
        flex 1
        .name
          margin-top 2px
          height 14px
          line-height 14px
          color rgb(7,17,27)
          font-size 14px
        .desc
        .extra
          margin-top 8px
          line-height 10px
          color rgb(147,153,159)
          font-size 10px
        .extra
          .count
            margin-right 12px
        .price
          font-weight 700
          line-height 24px
          .now
            margin-right 8px
            font-size 14px
            color rgb(240,20,20)
          .old
            font-size 10px
            color rgb(147,153,159)
            text-decoration line-through
</style>
