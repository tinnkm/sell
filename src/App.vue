<template>
  <div id="app">
    <div class="header">
      <v-header :seller="seller"></v-header>
    </div>
    <div class="tab">
      <div class="tab-item">
        <router-link :to="{path:'/goods'}" tag="a" active-class="active" >商品</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{path:'/ratings'}" tag="a" active-class="active">评论</router-link>
      </div>
      <div class="tab-item"><router-link :to="{path:'/seller'}" tag="a" active-class="active">商家</router-link></div>
    </div>
    <div class="content">
      <router-view/>
    </div>
  </div>
</template>

<script>
import VHeader from '@/components/header/Header'
const ERROR = 0
export default {
  data () {
    return {
      seller: {}
    }
  },
  name: 'App',
  components: {
    VHeader
  },
  created () {
    this.$http.get('/api/seller').then(
      (res) => {
        let data = res.body
        if (data.errno === ERROR) {
          this.seller = data.data
        }
      }
    )
  }
}
</script>

<style lang="stylus" scoped>
@import "common/stylus/mixin.styl"
#app
  .tab
    display flex
    width 100%
    height 40px
    line-height 40px
    border-1px(rgba(7,17,27,0.1))
    .tab-item
      flex 1
      text-align center
      & > a
        display block
        font-size 14px
        color rgb(77,85,93)
        &.active
          color rgb(240,20,20)
</style>
