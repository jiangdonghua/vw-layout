<template>
<div class="r-scroll" ref="scroll">
  <div class="r-scroll-wrap">
    <slot></slot>
  </div>
  <slot name="loading">
    <div v-show="isLoading" class="r-scroll-loading">
      <span class="r-scroll-loading-text">{{loadingText}}</span>
    </div>
  </slot>
  <slot name="complate">
    <div v-show="isComplate" class="r-scroll-loading">{{complateText}}</div>
  </slot>
</div>
</template>

<script type="text/ecmascript-6">

    export default{
        props:{
          // 距离底部数值，小于或等于该数值触发自定义事件loadmore
          bottomDistance: {
            type: [Number, String],
            default: 70
          },
          // 加载中的文字
          loadingText: {
            type: String,
            default: '加载中...'
          },
          // 数据加载完成的文字
          complateText: {
            type: String,
            default: '-- 我是个有底线的列表 --'
          },
          sw:true
        },
      data () {
        return {
          // 用来判定数据是否加载完成
          isComplate: false,
          // 用来判定是否正在加载数据
          isLoading: false,
          // 组件容器
          scroll: null,
          // 正文容器
          scrollWrap: null,
          open:true,
          one:true
        }
      },
      watch: {
        // 监听isLoading，如果isLoading的值为true则代表触发了loadmore事件
//        isLoading (val) {
//          if (val) {
//              console.log(val)
//            this.$emit('loadmore')
//          }
//        }
      },
      computed:{
            switchOpen(){
                return this.open=this.sw
        }
      },
      methods:{
        // 初始化组件，获取组件容器、正文容器节点，并给组件容器节点绑定滚动事件
            init(){
              this.scroll=this.$refs.scroll
              this.scrollWrap=this.scroll.childNodes[0]
             window.addEventListener('scroll',this.scrollEvent)
              this.$emit('init',this.scroll)
            },
        scrollEvent(e){
          // 如果数据全部加载完成了，则再也不触发loadmore事件
          if(this.isComplate) return
          let scrollTop=document.documentElement.scrollTop // 滚动高度
//          let offsetTop=this.scroll.offsetTop
         let offsetHeight=document.querySelector('.page-content').offsetHeight
          let wHeight= window.innerHeight
          let sHeight=this.scrollWrap.offsetHeight
          let scrollWrapH=this.scrollWrap.offsetTop
          // 组件容器滚的距离 + 组件容器本身距离大于或者等于正文容器高度 - 指定数值 则触发loadmore事件
//          两种方式
//          1.全加载在分页 感觉没卵用
//          if(scrollTop+wHeight>offsetHeight-this.bottomDistance){
//            if(this.switchOpen){
//              this.isLoading=true
//              if(this.one){
//                this.$emit('loadmore')
//                this.one=false
//              }else{
//                this.$emit('loadRest')
//              }
//            }
//          }
//          2.逐页请求
          if (scrollTop + wHeight > offsetHeight - this.bottomDistance) {
            if (this.switchOpen) {
              this.isLoading = true
                this.$emit('loadmore')
              }
            }
        },
        loaded(){
          // 所有数据加载完成后调用该函数
          this.isLoading=false
          this.isComplate=true
         window.removeEventListener('scroll',this.scrollEvent)
        }

      },
      mounted(){
            this.$nextTick(this.init)
      }
    }
</script>

<style lang="stylus" scoped>

</style>
