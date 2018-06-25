<template>
  <section class="CheapChannel-wrapper" w-750-312 aspectratio>
    <div aspectratio-content class="CheapChannel">
      <div v-for="(item,index) in list" :key="item.spm" class="border-right CheapChannel-left" v-if="!item.titleLabel">
        <a :href="item.href">
          <p class="titleImage"><img :src="item.titleImage" alt=""></p>
          <p class="subTitle">{{item.subTitle}}</p>
          <p class="image" w-327-132 aspectratio><img :src="item.image" alt="" aspectratio-content>
            <span class="minItemPrice">{{item.minItemPrice}}></span></p>
        </a>
      </div>
      <div class="CheapChannel-right">
        <div v-for="(item,index) in list" :key="item.spm" v-if="item.titleLabel" :class="`cheap-${index}`">
          <a :href="item.href" v-if="!item.image" class="item border-bottom">
            <div>
              <p class="titleImage fl"><img :src="item.titleImage" alt=""></p>
              <p class="titleLabel fr">{{item.titleLabel}}</p>
            </div>
            <div>
              <p class="subTitle fl">{{item.subTitle}}</p>
              <p class="minItemPrice fr">{{item.minItemPrice}}></p>
            </div>
          </a>
          <a :href="item.href" v-if="item.image" class="item right-bottom clearfix">
            <div class="text-wrapper fl">
              <p class="titleImage"><img :src="item.titleImage" alt=""></p>
              <p class="subTitle">{{item.subTitle}}</p>
              <p><span class="minItemPrice ignore fl">{{item.minItemPrice}}</span>
                <span class="titleLabel ignore fl">{{item.titleLabel}}</span>
              </p>
            </div>
            <div class="image-wrapper fr">
              <p class="image"><img :src="item.image" alt=""></p>
            </div>
          </a>

        </div>
      </div>

    </div>
  </section>
</template>

<script type="text/ecmascript-6">

  export default{
    name: 'CheapChannel',
    props: {
      list: Array
    },
    data(){
      return {}
    },
    created(){

    }
  }
</script>

<style lang="stylus" scoped>
  @import "~assets/stylus/border.styl"
  @import "~assets/stylus/mixins.styl"
  .CheapChannel-wrapper
    margin: 12px 0;
  [w-750-312]
    aspect-ratio: '750:312'
  .CheapChannel
    display: flex
    font-size: 26px
    background-color: #fff
    & > div
      flex: 1
      padding: 24px 0 10px 0
    .CheapChannel-left
      display: flex
      .titleImage
        flex: 1
        height: 32px
      .subTitle
        height: 32px
        line-height: 32px
        font-size: 26px
        width: 327px
        margin: 15px auto
        ellipsis()
      [w-327-132]
        aspect-ratio: '327:132'
      .image
        position: relative
        width: 327px
        margin: 52px auto 0 auto
      .minItemPrice
        position: absolute
        top: -15px
        left: -1px
        font-size: .34667 * 75px;
        line-height: .4 * 75px;
        height: .4 * 75px;
        padding: .12 * 75px .24 * 75px;
        display: inline-block;
        border-radius: .32 * 75px 0 .32 * 75px .32 * 75px;
        background-image: -webkit-linear-gradient(left, orange, #ff5100);
        color: #fff;
        letter-spacing: 0;
    .CheapChannel-right
      .item
        display: block
        & > div
          padding: 0 18px 15px 18px;
          overflow: hidden
          &:last-child
            padding-bottom: 18px
        .titleImage
          width: 216px
          height: 32px
          margin-left: -18px;
        .subTitle
          height: 32px
          line-height: 32px
          font-size: 26px
          ellipsis()
        .image
          position: relative
          width: 132px
          height: 132px
          margin: 35px auto 0 auto
        .minItemPrice
          line-height: 30px;
          height: 30px;
          display: inline-block;
          border-radius: 24px 0 24px 24px;
          color: #ff5000;
          letter-spacing: 0
        .titleLabel
          color: #ff5000
          border: 1px solid #ff5000
          border-radius: 10px
          padding: 2px 5px
          line-height: 32px
        &.right-bottom
          .subTitle
            width: 188px
          .titleLabel, .minItemPrice
            max-width: 90px
            ellipsis()
          .minItemPrice
            font-size: 20px
            font-weight: bold
            margin-right: 5px
            height: 28px
            margin-top :3px
            /*line-height: 34px*/
            border: 1px solid transparent
          .image-wrapper
            padding-left: 0
            .image
              margin-top: 28px
          .text-wrapper
            padding: 18px 0 18px 18px
            p
              padding: 10px 0
              .titleLabel
                font-size: 20px
                height: 28px
                padding: 0 2px
                line-height: 30px

</style>
