<template>
  <section class="live-video" >
    <div class="title-bar" v-for="item in titleBar" w-750-110 aspectratio>
      <a :href="item.href"  aspectratio-content><img :src="item.titleImage" alt=""></a>
    </div>
    <div w-750-194 aspectratio>
      <div aspectratio-content class="wrapper">
        <a v-for="(item,index) in list" :style="`background-image:url(${item.image})`" class="video"  :href="item.href">
          <div class="base-bg"></div>
          <img v-lazy="item.titleIcon" alt="">
          <p class="ellipsis subTitle">{{item.subTitle}}</p>
          <p class="ellipsis title">{{item.title}}</p>
        </a>
      </div>

    </div>

  </section>
</template>

<script type="text/ecmascript-6">

  export default{
    name: 'LiveVideo',
    props: {
      list: Array,
      titleBar: Array
    },
    data(){
      return {
        bar: {}
      }
    },
    mounted(){
//      console.log(this.titleBar[0].titleImage)
    }
  }
</script>

<style lang="stylus" scoped>
  [w-750-110]
    aspect-ratio: '750:110'
  [w-750-194]
    aspect-ratio: '750:194'
  .live-video
    background-color: #ffffff
    .title-bar
      a
        display: block
        height: 110px
        img
          height: 110px
          display: block
   .wrapper
     display: flex
     padding 0 24px
     justify-content space-between
     box-sizing border-box
    .video
      position relative
      width: 345px;
      height: 194px;
      flex :0 0 345px
      background-repeat: no-repeat;
      background-position: center;
      background-size: cover;
      .base-bg
        position: absolute
        width: 100%
        height: 100%
        background-image: linear-gradient(180deg,transparent 50%,rgba(0,0,0,.3));
        background-repeat: repeat-x;
      p
        color #fff
        position: absolute
        z-index 3
        max-width :300px
        padding-left:18px
        line-height: 50px
        &.subTitle
          font-size: 30px
          bottom:50px
        &.title
          font-size:22px
          bottom:6px
      img
        position: absolute;
        top: 12px;
        right: 0;
        display: block;
        height: 35px;
        width: 140px;
        -webkit-box-flex: 1;
        background-size: contain;
        background-position: 0;
        background-repeat: no-repeat;
</style>
