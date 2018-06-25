<template>
  <header class="ignore header">
    <div class="header-left fl">
      <router-link to="/user" class="link">
        <span class="fly-icon icon-wode ignore"></span>
      </router-link>
    </div>

    <div class="header-input ignore">
      <router-link to="/search" class="link">
        <i class="fly-icon icon-sousuo"></i>
        <span class="text">输入城市/景点/游玩主题</span>
      </router-link>
    </div>

    <div class="header-right ignore fr">
      <router-link to="/city" class="link">
        <span class="nav-city">
          <i class="city">杭州</i>
          <i class="fly-icon icon-arrowdown"></i>
        </span>
      </router-link>
    </div>

  </header>
</template>

<script type="text/ecmascript-6">
  export default{
    name: 'HomeHeader',
  }
</script>

<style lang="stylus" scoped>
  @import "~assets/stylus/variables.styl"
  .header
    display: flex
    background: $bgColor
    /*position: absolute*/
    width: 100%
    /*z-index 40*/
    /*left: 0*/
    /*top: 0*/
    &.ignore
      height: 40px
      line-height: 40px
    .link
      display: block
      height: 100%
      color: #fff
    .header-left
      .icon-wode.ignore
        font-size: 22px
        padding 0 10px

    .header-input
      background-color: #fff
      flex 1
      &.ignore
        height: 26px
        line-height: 26px
        margin: 7px 0
        border-radius: 10px
        .link
          padding-left: 10px
          font-size: 14px
          color: rgba(61, 61, 61, .5)
    .header-right
      text-align: right
      &.ignore
        max-width: 70px
        overflow: hidden
        padding: 0 10px
        .link
          font-size: 14px
          .nav-city
            display: flex
            height: 100%


</style>
