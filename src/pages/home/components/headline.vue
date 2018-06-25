<template>
  <section class="HeadLine" flexcontainer w-750-108 aspectratio>
    <div aspectratio-content class="HeadLine-title" :style="{backgroundImage: `url(${attr.bgImage})`}">
      <swiper :options="swiperOption" ref="mySwiper" v-if="showSwiper" class="swiper-no-swiping">
        <swiper-slide v-for="(item,index) in list" :key="item.spm">
          <a class="news" :href="item.href">
            <div class="center">
              <p><i class="tag border">{{item.tag1}}</i><span class="desc">{{item.title1}}</span></p>
              <p><i class="tag border">{{item.tag2}}</i><span class="desc">{{item.title2}}</span></p>
            </div>
            <p w-144-108 aspectratio class="w-144-108">
              <img :src="item.image" aspectratio-content style="z-index: -1"/>
            </p>

          </a>
        </swiper-slide>
      </swiper>
      <div>
      </div>
    </div>

  </section>
</template>

<script type="text/ecmascript-6">

  export default{
    name: 'HeadLine',
    props: {
      list: Array,
      attr: Object
    },

    computed: {
      showSwiper(){
        return this.list.length
      },
    },
    data(){
      return {
        swiperOption: {
          autoplay: {
            disableOnInteraction: false,
          },
          direction: 'vertical',
          loop: true,
        },

      }
    }
  }
</script>

<style lang="stylus" scoped>
  @import '~assets/stylus/border.styl'
  @import '~assets/stylus/mixins.styl'

  [w-750-108]
    aspect-ratio: '750:108'

  .w-144-108
    aspect-ratio: '144:108'

  .w-144-108
    flex: 0 0 144px
    width: 144px
    img
      width: 144px
      height: 108px

  .HeadLine
    background-color #fff
    display: flex
    .HeadLine-title
      width: 100%
      /*flex: 0 0 168px*/
      height: 108px
      background-size: 100% 100%
      overflow: hidden
      .swiper-container
        height: 100%
        .news
          display: flex
          height: 108px
          padding-left: 126px
          font-size: 24px
          overflow: hidden
          line-height: 48px
          .center
            flex: 1
            padding: 8px 0 4px 0
            box-sizing: border-box
            box-shadow: 50px 0 50px -5px rgba(255, 255, 255, .8);
            p
              width: 478px
              flex: 0 0 478px
              ellipsis()
              .tag
                padding: 2px 8px
                margin-right: 8px
                color: #ff5038
                border: 1px solid #ff5038


</style>
