<template>
  <div>
    <router-link
      to="/"
      v-show="showAbs"
    >
      <div class="header-abs">
        <div class="iconfont header-abs-back">&#xe624;</div>
      </div>
    </router-link>
    <div class="header-fixed" v-show="!showAbs" :style="opacityStyle">
      景点详情
      <router-link to="/">
        <div class="iconfont header-fixed-back">&#xe624;</div>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 1
      }
    }
  },
  methods: {
    handleScroll () {
      let top = document.documentElement.scrollTop
      if (top > 60) {
        this.showAbs = false
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = {opacity}
      } else {
        this.showAbs = true
      }
    }
  },
  mounted () {
    window.addEventListener('scroll', this.handleScroll)
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll)
  }

}
</script>

<style lang="stylus" scoped>
  @import "~styles/variables.styl"
  .header-abs
    position: absolute
    left: .2rem
    top: .2rem
    width: .8rem
    height: .8rem
    border-radius: 50%
    line-height: .8rem
    text-align: center
    background: rgba(0,0,0,.8)
    .header-abs-back
      color: #fff
      font-size: .4rem
  .header-fixed
    position: fixed
    z-index: 2
    top: 0
    left: 0
    right: 0
    height: $headerHeight
    line-height: .86rem
    text-align: center
    color: #fff
    background: $bgColor
    font-size: .32rem
    .header-fixed-back
      position: absolute
      left: 0
      top: 0
      width: .64rem
      text-align: center
      font-size: .35rem
      color: #fff
</style>
