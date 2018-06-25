<template>
  <div class="page-content">
    <home-header></home-header>
    <home-banner :list="trip_home_banner" ></home-banner>
    <home-category :list="trip_home_entry"></home-category>
    <head-line :list="trip_home_travel_headline" :attr="trip_home_travel_headline_attr"></head-line>
    <cheap-channel :list="trip_home_cheap_channel" ></cheap-channel>
    <home-super :list="trip_home_travel_supermarket_title" :listentry="trip_home_travel_supermarket_entry"></home-super>
    <supermarket-product :list="trip_home_travel_supermarket_product"></supermarket-product>
    <supermarket-banner :list="trip_home_travel_supermarket_banner"></supermarket-banner>
    <live-video :list="trip_home_live_video" :titleBar="trip_home_live_video_title_bar"></live-video>
    <first-site :list="trip_home_global_first_site_main" :titleBar="trip_home_global_first_site_title_bar" :list1="trip_home_global_first_site_product"></first-site>
    <travel-banner :list="trip_home_recommended_weekend_travel_banner"></travel-banner>
    <arbitrary-gate :list="trip_home_arbitrary_gate_product" :titleBar="trip_home_arbitrary_gate_title_bar"></arbitrary-gate>
    <hot-destination :list="trip_home_hot_destination_product" :titleBar="trip_home_hot_destination_title_bar"></hot-destination>
    <may-favor @favorLoad="loadBottom"></may-favor>
    <home-bottom v-if="show"></home-bottom>
    <back-to-top></back-to-top>
  </div>

</template>

<script>
  import axios from 'axios'
  import HomeHeader from './components/header.vue'
  import HomeBanner from './components/banner.vue'
  import HomeCategory from './components/category.vue'
  import HeadLine  from  './components/headline.vue'
  import CheapChannel  from  './components/cheapchannel.vue'
  import HomeSuper  from  './components/supermarket.vue'
  import supermarketProduct  from  './components/supermarket-product.vue'
  import SupermarketBanner from "./components/supermarket-bannner.vue"
  import LiveVideo from "./components/live-video.vue"
  import FirstSite from './components/first-site.vue'
  import travelBanner from './components/weekend-travel-banner.vue'
  import arbitraryGate from './components/arbitrary-gate.vue'
  import hotDestination from './components/hot-destination.vue'
  import mayFavor from './components/may-favor.vue'
  import homeBottom from './components/bottom.vue'
  import backToTop from 'base/backToTop.vue'
  export default {
    name: 'Home',
    data () {
      return {
        city: "杭州",
        lastCity: '杭州',
        trip_home_titlebar: [],
        trip_home_banner: [],
        trip_home_entry: [],
        trip_home_travel_headline: [],
        trip_home_travel_headline_attr: {},
        trip_home_cheap_channel: [],
        trip_home_travel_supermarket_title:[],
        trip_home_travel_supermarket_entry:[],
        trip_home_travel_supermarket_product:[],
        trip_home_travel_supermarket_banner:[],
        trip_home_live_video_title_bar:[],
        trip_home_live_video:[],
        trip_home_global_first_site_title_bar:[],
        trip_home_global_first_site_main:[],
        trip_home_global_first_site_product:[],
        trip_home_recommended_weekend_travel_banner:[],
        trip_home_arbitrary_gate_title_bar:[],
        trip_home_arbitrary_gate_product:[],
        trip_home_hot_destination_title_bar:[],
        trip_home_hot_destination_product:[],
        show:false
      }
    },
    methods: {
      getHomeInfo(){
        axios.get('/api/index.json')
          .then(this.getHomeInfoSucc)
      },
      getHomeInfoSucc(res){
        const _this = this
        if (res.data.ret && res.data.data) {
          const HomeData = res.data.data.sections;

          HomeData.map((item, index) => {
            switch (item.id) {
              case 'trip_home_titlebar':
                _this.trip_home_titlebar = item.items;
                break;
              case 'trip_home_banner':
                _this.trip_home_banner = item.items;
                break;
              case 'trip_home_entry':
                _this.trip_home_entry = item.items;
                break;
              case 'trip_home_travel_headline':
                _this.trip_home_travel_headline = item.items;
                _this.trip_home_travel_headline_attr = item.attr;
                break;
              case 'trip_home_cheap_channel':
                _this.trip_home_cheap_channel = item.items;
                break;
              case 'trip_home_travel_supermarket_title':
                _this.trip_home_travel_supermarket_title = item.items;
                break;
              case 'trip_home_travel_supermarket_entry':
                _this.trip_home_travel_supermarket_entry = item.items;
                break;
              case 'trip_home_travel_supermarket_product':
                _this.trip_home_travel_supermarket_product = item.items;
                break;
              case 'trip_home_travel_supermarket_banner':
                _this.trip_home_travel_supermarket_banner = item.items;
                break;
              case 'trip_home_live_video_title_bar':
                _this.trip_home_live_video_title_bar = item.items;
                break;
              case 'trip_home_live_video':
                _this.trip_home_live_video = item.items;
                break;
              case 'trip_home_global_first_site_title_bar':
                _this.trip_home_global_first_site_title_bar = item.items;
                break;
              case 'trip_home_global_first_site_main':
                _this.trip_home_global_first_site_main = item.items;
                break;
              case 'trip_home_global_first_site_product':
                _this.trip_home_global_first_site_product = item.items;
                break;
              case 'trip_home_recommended_weekend_travel_banner':
                _this.trip_home_recommended_weekend_travel_banner = item.items;
                break;
              case 'trip_home_arbitrary_gate_title_bar':
                _this.trip_home_arbitrary_gate_title_bar = item.items;
                break;
              case 'trip_home_arbitrary_gate_product':
                _this.trip_home_arbitrary_gate_product = item.items;
                break;
              case 'trip_home_hot_destination_title_bar':
                _this.trip_home_hot_destination_title_bar = item.items;
                break;
              case 'trip_home_hot_destination_product':
                _this.trip_home_hot_destination_product = item.items;
                break;
            }
          })
        }
      },
      loadBottom(a){
          this.show=a
      },
      getTestInfo(){
        axios.get('/testApi',{
          headers: {
            referer: 'https://c.y.qq.com/',
            host: 'c.y.qq.com'
          },
            params:{
              g_tk: 5381,
              uin: 0,
              format: 'json',
              inCharset: 'utf-8',
              outCharset: 'utf-8',
              notice: 0,
              platform: 'h5',
              needNewCode: 1
            }
        })
          .then((res)=>{
            console.log(res)
            })
      },
    },
    mounted(){
      this.lastCity = this.city
      this.getHomeInfo()
      this.getTestInfo()
    },
    activated(){
      if (this.lastCity !== this.city) {
        this.lastCity = this.city
        this.getHomeInfo()
      }
    },
    components: {
      FirstSite, SupermarketBanner, HomeHeader,
      HomeBanner,
      HomeCategory,
      HeadLine,
      CheapChannel,
      HomeSuper,
      supermarketProduct,
      LiveVideo,
      travelBanner,
      arbitraryGate,
      hotDestination,
      mayFavor,
      homeBottom,
      backToTop
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
  .page-content
    position: absolute
    top: 0
    left: 0
    width: 100%
    min-height 100%
    background: #f5f5f5

</style>
