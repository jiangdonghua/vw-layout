<template>
  <section class="travel-banner border-top">
    <div class="banner-wrapper ignore" flexcontainer w-750-180 aspectratio>
      <div aspectratio-content>
        <swiper :options="swiperOption" ref="mySwiper" v-if="showSwiper">
          <swiper-slide v-for="(banner,index) in swiperList" :key="banner.spm">
            <a :href="banner.href"><img :data-src="banner.image" class="swiper-lazy"></a>
          </swiper-slide>
          <div class="swiper-pagination ignore" slot="pagination" id="swiper-pagination"></div>
        </swiper>
      </div>
    </div>
  </section>
</template>

<script type="text/ecmascript-6">

  export default{
    name: 'travelBanner',
    props: {
      list: Array
    },
    data(){
      return {
        swiperOption: {
          pagination: {
            el: '.swiper-pagination'
          },
          passiveListeners: false,
          loop: true,
          autoplay: {
            disableOnInteraction: false,
          },
          lazy: {
            loadPrevNext: true
          },
        },
        swiperList: []
      }
    },
    computed: {
      swiper(){
        return this.$refs.mySwiper.swiper
      },
      showSwiper(){
        return this.swiperList.length
      }
    },
    watch:{
      list:function (val,oldVal) {
        if(val){
          this.swiperList=val
        }

      }
    },
    mounted(){
//      console.log('this is current swiper instance object', this.swiper)
//      this.swiper.slideTo(3, 1000, false)
//      this.swiperList = this.list
    }
  }
</script>

<style lang="stylus" scoped>
.travel-banner
   padding :30px 0
   background-color #ffffff
  .banner-wrapper
    touch-action :none
    a
      display: block
  [w-750-180]
    aspect-ratio: '750:180'
  .swiper-pagination
    text-align :right
    right: 21px
    width auto
  img
    width: 100%
    height: 100%
  .banner-wrapper.ignore >>> .swiper-pagination-bullet
    width:10px
    height:6px
    margin:0 3px
    background:#ffc900
    opacity:0.5
  .banner-wrapper.ignore >>> .swiper-pagination-bullet-active
    background:#ffc900
    opacity:1
</style>
