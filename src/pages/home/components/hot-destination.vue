<template>
  <section class="hot-destination border-top">
    <div class="title-bar" v-for="item in titleBar" w-750-110 aspectratio>
      <a :href="item.href" aspectratio-content><img v-lazy="item.titleImage" alt=""></a>
    </div>
    <div w-750-304 aspectratio>
      <div aspectratio-content class="item-wrapper">
        <ul class="clearfix">
          <li v-for="(item,index) in list" class="regular_item">
            <a  :href="item.href">
              <div class="img-wrapper">
                <img v-lazy="item.image" alt="" class="item_img">
              </div>
              <div class="base-bg">
                <p class="title ellipsis">{{item.title}}</p>
                <p class="subTitle ellipsis">{{item.subTitle}}</p>
              </div>
            </a>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<script type="text/ecmascript-6">

    export default{
      name: 'hotDestination',
      props: {
        list: Array,
        titleBar: Array
      },
    }
</script>

<style lang="stylus" scoped>
  [w-750-110]
    aspect-ratio: '750:110'
  [w-750-304]
    aspect-ratio: '750:304'
  .hot-destination
    background-color #fff
    .item-wrapper
      padding: 0 24px 48px
      ul
        li
          float: left
          width: 232px
          height: 127px
          margin-right: 2px
          &:first-child
            width: 232px
            height: 256px
          &:nth-child(2),&:nth-child(3)
            margin-bottom: 2px
          a
            display: block
            position: relative
            .base-bg
              position: absolute
              z-index: 1
              top: 0
              left: 0
              width: 100%
              height: 100%
              background-image: linear-gradient(180deg,transparent 0,rgba(0,0,0,.3) 50%)
              background-repeat: repeat-x
              p
                margin-left:12px
                display: block
                color: #fff
                max-width: 200px
              .title
                margin-top: 16px
                font-size: 32px
                height: 40px
                line-height: 40px
              .subTitle
                font-size: 22px
                margin-top: 6px
                height: 36px
                line-height: 36px
                margin-bottom: 24px


</style>
