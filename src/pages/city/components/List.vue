<template>
    <div class="list" ref="wrapper">
        <div >
            <div class="area">
                <div class="title border-topbottom">当前城市</div>
                <div class="button-list">
                    <div class="button-wrapper">
                        <div class="button">{{ this.currentCity }}</div>
                    </div>
                </div>
            </div>
            <div class="area">
                <div class="title border-topbottom">热门城市</div>
                <div class="button-list">
                    <div class="button-wrapper" v-for="item of hot" :key="item.id" @click="handleCityClick(item.name)">
                        <div class="button">{{ item.name}}</div>
                    </div>
                </div>
            </div>
            <div
              class="area"
              v-for="(item,key)
              of cities"
              :key="key"
              :ref="key"
              >
                <div class="title border-topbottom">{{ key }}</div>
                <div class="item-list">
                    <div class="item border-bottom"
                      v-for="innerItem of item"
                      :key="innerItem.id"
                      @click="handleCityClick(innerItem.name)"
                      >
                      {{ innerItem.name }}</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import BScroll from 'better-scroll'
import { mapState, mapMutations } from 'vuex'
export default {
  name: 'CityList',
  props: {
    hot: Array,
    cities: Object,
    letter: String
  },
  computed: {
    ...mapState({
      currentCity: 'city'
    })
  },
  methods: {
    handleCityClick (city) {
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  watch: {
    letter () {
      if (this.letter) {
        const element = this.$refs[this.letter][0]
        this.scroll.scrollToElement(element)
      }
    }
  },
  mounted () { // 刚挂载完成
    this.scroll = new BScroll(this.$refs.wrapper, {
      click: true// 手机端点击对应的城市有反应
    })
  },
  updated () { // 一旦更新
    this.scroll.refresh()
  },
  activated () { // 缓存取出keep-alive
    this.scroll.refresh()
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .border-topbottom
    &:before
      border-color:#ccc
    &:after
      border-color:#ccc
  .border-bottom
    &:before
      border-color:#ccc
  .list
    overflow:hidden
    position:absolute
    top:1.58rem
    left:0
    right:0
    bottom: 0
    .title
      text-align: left
      line-height: .54rem
      background:#eee
      padding-left: .2rem
      color:#666
      font-size:.26rem
    .button-list
      overflow: hidden
      padding:.1rem .6rem .1rem .1rem
      .button-wrapper
        float:left
        width:33.33%
        .button
          margin:.1rem
          padding: .1rem 0
          border: .02rem solid #ccc
          border-radius: .06rem
    .item-list
      text-align: left
      .item
        text-align: left
        line-height: .76rem
        padding-left:0.2rem

</style>