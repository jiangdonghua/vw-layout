<template>
  <section class="product" w-750-226 aspectratio>
    <div aspectratio-content>
      <a v-for="(item,index) in list" :key="item.trackname" class="fade" :class="
  index===0?'product-left':'product-right'" :style="`background-image:url(${item.image})`">
        <p class="title ellipsis">{{item.title}}</p>
        <p v-if="index===0" class="subtitle ellipsis">{{item.subTitle}}</p>
        <div class="mask"></div>
      </a>
    </div>
  </section>
</template>

<script type="text/ecmascript-6">

  export default{
    name: 'supermarketProduct',
    props: {
      list: Array
    },
    mounted(){

    }
  }
</script>

<style lang="stylus" scoped>
  [w-750-226]
    aspect-ratio: '750:226'
    &>[aspectratio-content]
      display flex
      justify-content: space-between
      background-color: #fff
      padding :0 24px
      box-sizing :border-box
  .product
    .fade
      transition: opacity .25s ease-in 0s;
      -webkit-transition: opacity .25s ease-in 0s;
    & >div a
      display: block
      background-position: center
      background-size: cover
      background-repeat no-repeat
      height: 226px
      position:relative
    .product-left
      width: 464px
      flex: 0 0 464px
      color: #fff
      .title, .subtitle
        position: absolute
        width: 430px
        padding-left: 24px
        z-index 2
      .mask
        position absolute
        top: 0
        width: 100%
        height: 100%
        color: #fff
        background-image: linear-gradient(top, transparent 44%, rgba(0, 0, 0, 0.52) 92%)
        z-index: 0
      .title
        top: 120px
        font-size: 36px
      .subtitle
        top: 160px
        font-size: 26px
    .product-right
      width: 226px
      flex: 0 0 226px
      color: #333
      .title, .subtitle
        position: absolute
        width: 160px
        padding-left: 24px
        z-index 2
      .title
        bottom: 12px
        left: 12px
        padding 10px 22px
        background-image: linear-gradient(left, #ffe700, #ffc900)
        font-size: 32px
        border-radius: 30px 0 30px 30px
        text-align: center
        letter-spacing: 0
        width: 160px
</style>
