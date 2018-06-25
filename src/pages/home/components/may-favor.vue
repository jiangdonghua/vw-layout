<template>
  <section class="may-favor border-top">
    <div class="title-bar" v-for="item in trip_home_guess_favor_title_bar" w-750-110 aspectratio>
      <a :href="item.href" aspectratio-content><img v-lazy="item.titleImage" alt=""></a>
    </div>
    <div class="may-favor-cont">
      <r-scroll class="clearfix" @loadmore="loadmore" @loadRest="loadRest" @init="scroll" ref="rscroll" :sw="sw">
        <ul>
          <li v-for="(item,index) in home_guess_favor_contents" class="regular_item"
              v-if="home_guess_favor_contents.length">
            <a :href="item.href">
              <div class="img-wrapper">
                <img v-lazy="item.image" alt="" class="item_img" :key="item.image">
                <p class="type ellipsis">{{item.type}}</p>
              </div>
              <p class="title lineclamp">{{item.title}}</p>
              <div class="bottom">
                <p class="price">
                  <span>{{item.pricePrefix}}</span><strong>{{item.price}}</strong></p>
                <p class="desc">{{item.description}}</p>
              </div>
            </a>
          </li>
        </ul>
      </r-scroll>
    </div>
  </section>
</template>

<script type="text/ecmascript-6">
  import rScroll from 'base/r-scroll.vue'
  import axios from 'axios'
  export default{
    name: 'mayFavor',
    props: {
      list: Array,
      titleBar: Array
    },
    data(){
      return {
        i: 0,
        sw: true,
        page: 1,
        pageSize: 10,
        totalCount: [],
        trip_home_guess_favor_title_bar: [],
        trip_home_guess_favor_title_attr: [],
        trip_home_guess_favor_contents2: [],
        home_guess_favor_contents: []
      }
    },
    methods: {
      loadmore(){
        this.sw = false
        axios.get('/api/destination.more.json', {
          params: {
            page: this.page,
            pageSize: this.pageSize
          }
        })
          .then(this.getfavar)
      },
      getfavar(res){
        const _this = this
        if (res.data.ret && res.data.data) {
          const favorData = res.data.data.sections;
          favorData.map((item, index) => {
            switch (item.id) {
              case 'trip_home_guess_favor_title_bar':
                _this.trip_home_guess_favor_title_bar = item.items;
                _this.trip_home_guess_favor_title_attr = item.attr;
                break;
              case 'trip_home_guess_favor_contents2':
                _this.totalCount = item.totalCount;
                _this.trip_home_guess_favor_contents2 = item.items;
                break;
            }
          })
          _this.loadRest()
        }
      },
      loadRest(){
        const _this = this
        const Count = Math.ceil(_this.totalCount / _this.pageSize)
        if (_this.page < Count) {
          _this.home_guess_favor_contents = _this.trip_home_guess_favor_contents2.slice(0, _this.pageSize * (_this.page))
          _this.sw = true
          _this.page++
        } else {
          _this.$refs.rscroll.loaded()
          _this.$emit('favorLoad','true')
        }
      },

//      getfavar(res){
//        const _this = this
//        if (res.data.ret && res.data.data) {
//          const favorData = res.data.data.sections;
//          favorData.map((item, index) => {
//            switch (item.id) {
//              case 'trip_home_guess_favor_title_bar':
//                _this.trip_home_guess_favor_title_bar = item.items;
//                _this.trip_home_guess_favor_title_attr = item.attr;
//                break;
//              case 'trip_home_guess_favor_contents2':
//                _this.totalCount = item.totalCount;
//                _this.trip_home_guess_favor_contents2 = item.items;
//                break;
//            }
//          })
//          _this.home_guess_favor_contents = _this.trip_home_guess_favor_contents2.slice(0, _this.pageSize * (_this.page))
//          this.page++
//          this.sw = true
//        }
//      },
//      loadRest(){
//        this.sw = false
//        const _this = this
//        const Count = Math.ceil(_this.totalCount / _this.pageSize)
//        if (_this.page < Count+1) {
//          _this.home_guess_favor_contents = _this.trip_home_guess_favor_contents2.slice(0, _this.pageSize * (_this.page))
//          this.sw = true
//          console.log(_this.page)
//          _this.page++
//        } else {
//          this.$refs.rscroll.loaded()
//        }
//      },
      scroll(a){
        //console.log(a)
      }
    },
    components: {
      rScroll
    },
  }
</script>

<style lang="stylus" scoped>
  [w-750-110]
    aspect-ratio: '750:110'

  .may-favor
    margin-bottom: 20px
    .title-bar
      background-color #fff
    .may-favor-cont
      background-color #fff
      margin: 0 24px
      ul
        display: flex
        justify-content space-between
        flex-wrap wrap
        .regular_item
          width: 345px
          .img-wrapper
            position relative
            width: 345px
            height: 345px
            .item_img
              width: 345px
              height: 345px
            .type
              position absolute
              color: #fff
              top: 12px
              left: 12px
              font-size: 24px
              height: 48px
              line-height: 50px
              border-radius: 100px 0 100px 100px
              padding: 0 24px
              background-color: rgba(0, 0, 0, .6)
              max-width: 280px
          .title
            color: #333
            font-size: 26px
            line-height: 40px
            height: 80px
            font-weight: 400
            padding: 0 12px
          .bottom
            display: flex
            justify-content space-between
            align-items center
            padding: 0 24px 18px 12px
            margin-top: 2px
            position: relative
            box-sizing: border-box
            overflow: hidden
            .price
              color: #ff5000
              line-height: 1
              span, strong
                display: inline-block
                vertical-align: bottom
              span
                font-size: 20px
              strong
                font-weight: 400
                font-size: 36px
                position: relative
                bottom: -2px
            .desc
              display: block
              color: #a5a5a5
              font-size: 24px
              line-height: 32px

</style>
