<template>
  <div>
    <div class="banner" @click="handleBannerClick">
      <img class="banner-img" :src="bannerImg">
      <div class="banner-info">
        <div class="banner-title">{{ this.sightName }}</div>
        <div class="banner-number">
          <span class="iconfont banner-icon">&#xe67f;</span>{{ this.gallaryImgs.length }}
        </div>
      </div>
    </div>
    <fade-animation>
      <common-gallary :imgs="gallaryImgs" v-show="showGallary" @close="handleGallaryClose"></common-gallary>
    </fade-animation>
  </div>
</template>

<script>
import CommonGallary from 'common/gallary/Gallary'
import FadeAnimation from 'common/fade/FadeAnimation'
export default {
  name: 'Banner',
  props: {
    sightName: String,
    bannerImg: String,
    gallaryImgs: Array
  },
  components: {
    CommonGallary,
    FadeAnimation
  },
  data () {
    return {
      showGallary: false
    }
  },
  methods: {
    handleBannerClick () {
      this.showGallary = true
    },
    handleGallaryClose () {
      this.showGallary = false
    }
  }
}
</script>

<style lang="stylus" scoped>
  .banner
    position:relative
    overflow: hidden
    height: 0
    padding-bottom: 55%
    .banner-img
      width: 100%
    .banner-info
      display: flex
      position:absolute
      left: 0
      right: 0
      bottom:0
      line-height: .6rem
      color:#fff
      background-image:linear-gradient(to top,rgba(0,0,0,0),rgba(0,0,0,0.8))
      .banner-title
        flex:1
        font-size:.32rem
        text-align: left
        padding: 0 .2rem
      .banner-number
        height: .32rem
        margin: .14rem
        padding: 0 .4rem
        line-height: .32rem
        border-radius: .2rem
        background:rgba(0,0,0,.8)
        font-size:.24rem
        .banner-icon
          font-size:.24rem

</style>