<template>
  <section class="first-site">
    <div class="title-bar" v-for="item in titleBar" w-750-110 aspectratio>
      <a :href="item.href" aspectratio-content><img v-lazy="item.titleImage" alt=""><span
        class="rightText">{{item.rightText}}</span></a>
    </div>
    <div w-750-256 aspectratio>
      <div aspectratio-content class="wrapper">
        <a v-for="(item,index) in list" :href="item.href">
          <div class="site-left">
            <p class="ellipsis tag">{{item.tag}}</p>
            <p class="title">{{item.title}}</p>
            <p class="line"></p>
            <p class="ellipsis subTitle">{{item.subtitle}}</p>
          </div>
          <img v-lazy="item.image" alt="" class="site-right">
        </a>
      </div>
    </div>
    <div w-750-256 aspectratio>
      <div aspectratio-content class="item-wrapper">
        <div>
          <a v-for="(item,index) in list1" class="regular_item" :href="item.href">
            <div class="img-wrapper">
              <img v-lazy="item.image" alt="" class="item_img">
              <p class="ellipsis tag">{{item.tag}}</p>
            </div>
            <p class="title">{{item.title}}</p>
          </a>
        </div>

      </div>
    </div>
  </section>
</template>

<script type="text/ecmascript-6">

  export default{
    name: 'firstSite',
    props: {
      list: Array,
      list1: Array,
      titleBar: Array
    },
    created(){

    }
  }
</script>

<style lang="stylus" scoped>
  [w-750-110]
    aspect-ratio: '750:110'
  [w-750-256]
    aspect-ratio: '750:256'
  .first-site
    background-color #fff
    .title-bar
      .rightText
        position: absolute
        right: 36px
        top: 50%
        transform: translate(-50%, -50%)
        font-size: 16px
    .wrapper
      & > a
        display: flex
        padding 0 24px
        position: relative
        .site-right
          width: 464px
          height: 256px
          flex: 0 0 464px
        .site-left
          position relative
          /*flex 1*/
          background-color #f2f3f5
          padding-left: 12px
          .tag
            position: absolute
            background-color: #ffc900
            max-width: 200px
            left 12px
            padding: 0 12px
            height: 48px
            line-height: 48px
            font-size: 24px
            color: #3d3d3d
          .title
            margin-top 90px
            width: 90%
            font-size: 30px
            line-height: 36px
            -webkit-line-clamp: 3
            word-break: break-all
            overflow: hidden
            height: 106px
          .line
            display: -webkit-box;
            height: 1px
            margin-top: 12px
            width: 60px
            background-color: #ffc900
            border-radius: 12px
          .subTitle
            font-size: 14px
            margin-top: 10px
            color: #a5a5a5
            height: 33px
            line-height: 33px
    .item-wrapper
      margin-top: 15px
      &>div
        display: flex
        justify-content space-between
        padding 0 24px
      .regular_item
        width: 226px
        flex: 0 0 226px
        .img-wrapper
          position relative
          width: 226px
          height: 128px
          .tag
            position absolute
            left: 0
            bottom: 0
            display: inline-block
            font-size: 22px
            height: 30px
            max-width: 200px
            line-height:30px
            padding: 9px 12px
            color: #fff
            background-color: rgba(0,0,0,.6)


        .title
          display: -webkit-box
          -webkit-line-clamp: 2
          word-break: break-all
          overflow: hidden
          margin-bottom: 24px
          width: 214px
          margin-top: 18px
          line-height: 36px
          height:72px
          font-size: 24px
          color: #3d3d3d
</style>
