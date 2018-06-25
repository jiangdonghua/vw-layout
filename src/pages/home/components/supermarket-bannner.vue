<template>
  <section class="supermarket-banner">
    <div v-for="(item,index) in list" class="base-bg">
      <a :style="`background-image:url(${item.image})`" :href="item.href"></a>
    </div>
  </section>
</template>

<script type="text/ecmascript-6">

  export default{
    name: 'supermarketBanner',
    props: {
      list: Array
    }
  }
</script>

<style lang="stylus" scoped>
.base-bg
  position: relative;
  padding: 12px 24px 36px;
  width: 702px;
  height: 72px;
  background-color: #fff;
  &>a
    display: block
    width: 100%
    height: 100%
    background-repeat: no-repeat
    background-position: 50%
    background-size: cover
</style>
