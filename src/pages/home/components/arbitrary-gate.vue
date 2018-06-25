<template>
  <section class="arbitrary-gate border-top">
    <div class="title-bar" v-for="item in titleBar" w-750-110 aspectratio>
      <a :href="item.href" aspectratio-content><img v-lazy="item.titleImage" alt=""></a>
    </div>
    <div w-750-512 aspectratio>
      <div aspectratio-content class="item-wrapper">
        <div class="clearfix">
          <a v-for="(item,index) in list" class="regular_item" :href="item.href">
            <div class="img-wrapper">
              <img v-lazy="item.image" alt="" class="item_img">
            </div>
            <p class="title ellipsis">{{item.title}}</p>
            <p class="subTitle ellipsis">{{item.subTitle}}</p>
          </a>
        </div>
        </div>
    </div>
  </section>
</template>

<script type="text/ecmascript-6">

  export default{
    name: 'arbitraryGate',
    props: {
      list: Array,
      titleBar: Array
    },
    created(){

    }
  }
</script>

<style lang="stylus" scoped>
  [w-750-110]
    aspect-ratio: '750:110'
  [w-750-512]
    aspect-ratio: '750:512'
  .arbitrary-gate
    background-color #fff
    .item-wrapper
      &>div
        padding 0 24px
      .regular_item
        width: 226px
        float: left
        margin-right 12px
        &:nth-child(3n)
          margin-right: 0
        .img-wrapper
          position relative
          width: 226px
          height: 128px
          img
            height: 128px
        .title
          display: inline-block
          font-size: 28px
          height: 40px
          line-height: 40px
          margin-top: 12px
          color: #3d3d3d;
          max-width: 200px
        .subTitle
          display: inline-block
          font-size: 24px
          color: #a5a5a5
          margin-top: 6px
          height: 36px
          line-height: 36px
          margin-bottom: 24px
          max-width: 200px
</style>
