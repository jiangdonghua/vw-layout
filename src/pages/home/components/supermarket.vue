<template>
  <section class="supermarket">
    <div v-for="(item,index) in list" :key="item.trackname">
      <a class="title" :style="`backgroundImage:url(${item.titleImage})`" :href="item.href">
{{item.rightText}}
      </a>
      <ul class="clearfix ellipsis entryUl">
        <li v-for="(entry,index) in listentry" :key="entry.trackname" class="entryLi"><a :href="entry.href">{{entry.title}}</a></li>
      </ul>
    </div>

  </section>
</template>

<script type="text/ecmascript-6">

  export default{
    name: 'HomeSuper',
    props: {
      list: Array,
      listentry:Array
    }
  }
</script>

<style lang="stylus" scoped>
.supermarket
  background-color :#fff
  height: 200px
  .title
    display: block
    background-size :100% 100%
    background-repeat :no-repeat
    height: 93px
    text-align :right
    padding-right: 60px
    line-height: 106px
    font-size: 26px
    color: #666
  .entryUl
    margin-bottom: .24rem
    height: 60px
    padding-left:24px
    .entryLi
      float: left
      height: 60px
      margin-right: 20px
      line-height: 60px
      margin-bottom: 24px
      text-align: center
      border-radius: 100px
      -webkit-box-sizing: border-box
      color: #666;
      font-weight: 400;
      box-sizing: border-box
      position: relative
      font-size: 24px
      border: 1px solid #fca500
      a
        display: block
        padding: 0 22px
</style>
