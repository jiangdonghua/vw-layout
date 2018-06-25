<template>
  <section class="category-wrapper ignore"flexcontainer w-750-432 aspectratio>
    <div aspectratio-content>
      <swiper :options="swiperOption" ref="mySwiper" v-if="showSwiper">
        <swiper-slide v-for="(page,index) in pages" :key="index">
          <div v-for="(item,index) in page" :key="item.spm" class="wrapper">
          <a :href="item.href" class="icon" >
            <div class="icon-img"><img :src="item.image" :alt="item.spm"></div>
            <p class="icon-desc" v-text="item.title"></p>
            <i v-if="item.corner" class="corner">{{item.corner}}</i>
          </a>
          </div>
        </swiper-slide>

      </swiper>
      <div class="swiper-pagination ignore" slot="pagination" id="swiper-pagination"></div>
    </div>

  </section>
</template>

<script type="text/ecmascript-6">
  export default{
    name: 'HomeCategory',
    props:{
      list:Array
    },
    data(){
      return {
        swiperOption: {
          pagination: {
            el: '.swiper-pagination'
          },
          passiveListeners: false,
          loop: false,
          auutoplay:false
        },

      }
    },
    computed: {
      swiper(){
        return this.$refs.mySwiper.swiper
      },
      showSwiper(){
        return this.list.length
      },
      pages(){
         const pages=[]
        this.list.forEach((item,index)=>{
             const page=Math.floor(index/8)
          if(!pages[page]){
            pages[page]=[]
          }
          pages[page].push(item)

        })

        return pages
      }
    },

    mounted(){
//      console.log('this is current swiper instance object', this.swiper)
//      this.swiper.slideTo(3, 1000, false)

    }
  }
</script>

<style lang="stylus" scoped>
  @import '~assets/stylus/mixins.styl'
  .category-wrapper
      background-color :#fff
      touch-action :none
  .category-wrapper .ignore >>> .swiper-pagination-bullet
    width:8px
    height:8px
    margin:0 3px
    background:#ffc900
    opacity:0.5
  .category-wrapper.ignore >>> .swiper-pagination-bullet-active
    background:#ffc900
    opacity:1
  [w-750-432]
    aspect-ratio: '750:360'
  .swiper-container
    bottom :0
  .swiper-pagination
    position: absolute
    width: 100%
    text-align :center
    bottom:20px
  .swiper-slide
    display :flex
    flex-wrap wrap;
  .wrapper
    position: relative
    width: 20%
    float: left
    flex:0 0 20%
    .icon
      .icon-img
        img
          width: 100%
          height: 100%
      .icon-desc
        text-align :center
        font-size: 24px
        line-height: 32px
        ellipsis()
      .corner
        background :#ff5000
        color: #ffffff
        font-size: 18px
        border-radius :20px
        padding :4px 5px
        position :absolute
        right :0
        top:24%



</style>
