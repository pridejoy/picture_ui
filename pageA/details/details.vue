<template>
  <view class="template-details">
    <!-- 顶部自定义导航 -->
    <tn-nav-bar fixed alpha customBack>
      <view slot="back" class='tn-custom-nav-bar__back'
        @click="goBack">
        <text class='icon tn-icon-left'></text>
        <text class='icon tn-icon-home-capsule-fill'></text>
      </view>
    </tn-nav-bar>
    
    <view class="">
      <view class="icon15__item--icon tn-flex tn-flex-row-center tn-flex-col-center tn-shadow-blur button-3" @tap="showLandscape">
        <view class="tn-icon-level"></view>
      </view>
      <view class="icon15__item--icon tn-flex tn-flex-row-center tn-flex-col-center tn-shadow-blur button-2" @click="tn('/pageA/author/author')">
        <view class="tn-icon-my"></view>
      </view>
      <view class="icon15__item--icon tn-flex tn-flex-row-center tn-flex-col-center tn-shadow-blur button-1" @click="tn('/pageB/chat/chat')">
        <view class="tn-icon-comment"></view>
      </view>
    </view>  
    
    
    <!-- 页面内容 -->
	<view class="slideshow">
		<template v-for="(item, index) in swiperList">
			<view class="slideshow-image"  @click="imagePreview(index)" :style="'background-image:url('+ item.url + item.path + ');'"></view>
		</template>	</view>
	<!-- <swiper class="card-swiper" :circular="true"
      :autoplay="true" duration="500" interval="12000" @change="cardSwiper" > 
      <swiper-item v-for="(item,index) in swiperList" :key="index" :class="cardCur==index?'cur':''">
        <view class="swiper-item image-banner" @click="$func.imagePreview(item.url + item.path)" :style="'background-image:url('+ item.url + item.path + ');background-size: cover;border-radius: 15rpx;background-repeat: no-repeat;'">
        </view>
      </swiper-item>
    </swiper>
    <view class="indication">
        <block v-for="(item,index) in swiperList" :key="index">
            <view class="spot" :class="cardCur==index?'active':''"></view>
        </block>
    </view> -->
    
    
    <!-- 底部tabbar start-->
    <view class="tabbar footerfixed dd-glass tn-color-white" style="border-radius: 100rpx;">
      <view class="action">
        <view class="bar-icon">
          <view class="tn-icon-like-lack">
          </view>
          <!-- <image class="" src='https://tnuiimage.tnkjapp.com/tabbar/a1.png'></image> -->
        </view>
        <view class="">收藏</view>
      </view>
      <view class="action" @click="downloadImageHandle">
        <view class="bar-icon">
          <view class="tn-icon-download">
          </view>
          <!-- <image class="" src='https://tnuiimage.tnkjapp.com/tabbar/k2.png'></image> -->
        </view>
        <view class="">下载</view>
      </view>
      <view class="action">
        
        <view class="bar-icon">
          <view class="tn-icon-flower">
          </view>
          <!-- <image class="" src='https://tnuiimage.tnkjapp.com/tabbar/i2.png'></image> -->
        </view>
        <view class="">海报</view>
      </view>
      <view class="action">
        <button class="tn-flex-direction-column tn-flex-row-center tn-flex-col-center tn-button--clear-style" open-type="share">
          <view class="bar-icon">
            <view class="tn-icon-send">
            </view>
            <!-- <image class="" src='https://tnuiimage.tnkjapp.com/tabbar/d2.png'></image> -->
          </view>
          <view class="">分享</view>  
        </button>
      </view>
    </view>
    
    <!-- 压屏窗-->
    <tn-landscape :show="show1" @close="closeLandscape" closePosition="bottom" :closeSize="60">
      <view class="tn-color-white" style="width: 100vw;">
        
        <view class="" style="margin: 120rpx 60rpx;">
          <view class="tn-flex tn-flex-col-top">
        
            <view class="">
              <view class="logo-pic tn-shadow">
                <view class="logo-image">
					<view class="tn-shadow-blur" :style="'background-image:url('+ swiperList[0].author.qr_url +');width: 100rpx;height: 100rpx;background-size: cover;'">
                  </view>
                </view>
              </view>
              <view class="tn-icon-sex-male" style="position: absolute;margin: -105rpx 0 0 72rpx;border-radius: 100rpx;background-color: #FFFFFF;color: #FF71D2;padding: 5rpx;"></view>
            </view>
            <view class="tn-padding-left-sm tn-padding-top-xs" style="width: 100%;">
              <view class="tn-flex tn-flex-row-between tn-flex-col-between">
                <view class="justify-content-item">
                  <text class="tn-text-lg tn-text-bold">{{swiperList[0].user.nickname}}</text>
                  <text class="tn-padding-left-sm tn-padding-right-xs">水瓶座</text>
                  <text class="tn-icon-con-virgo"></text>
                </view>
                <view class="justify-content-item tn-round tn-text-xs tn-bg-orangered--light tn-color-orangered" style="padding: 5rpx 15rpx;">
                  <text class="tn-icon-warning-fill tn-padding-right-xs"></text> 举报
                </view>
              </view>
              <view class="tn-padding-top-xs">
                <view class="">
                  <text class="tn-text-df tn-color-gray--light">{{swiperList[0].upload_time}}</text>
                </view>
              </view>
            </view>
          </view>
        
          
          <view class="tn-flex tn-flex-row-between tn-flex-col-between tn-margin-top-xl tn-text-justify">
            <text class="">一个人所能做的就是做出好榜样，要有勇气在风言风语的社会中坚定地高举伦理的信念。——爱因斯坦</text>
          </view>
        </view>
  
        
      </view>
    </tn-landscape>
    
  </view>
</template>

<script>
  import template_page_mixin from '@/libs/mixin/template_page_mixin.js'
	import { imageItemList, imageDownLoad } from '@/utils/api/image'
	
  export default {
    name: 'TemplateDetails',
    mixins: [template_page_mixin],
    data(){
      return {
        show1: false,
        cardCur: 0,
        swiperList: [],
				image_uid: '',
      }
    },
		onLoad(options) {
			this.image_uid = options.image_uid || ""
			this.getImageItemList()
		},
    methods: {
			getImageItemList() {
				imageItemList({image_uid: this.image_uid}).then(res => {
					this.swiperList = res.items
				})
			},
      // 跳转
      tn(e) {
        uni.navigateTo({
          url: e,
        })
      },
			imagePreview(index) {
				this.cardCur = index
				this.downloadImageHandle()
			},
			downloadImageHandle() {
				let _that = this
				let cache = uni.getStorageSync('downloadimage')
				if (!cache) {
					uni.showModal({
						title: '下载提示',
						content: '默认下载第一张，下载指定图片，请点击对应的图片',
						confirmText: '知道了',
						cancelText: '关闭',
						success(res) {
							if (res.confirm) {// 点击确认
								uni.setStorageSync('downloadimage', 1)
							}
							_that.downloadImage()
						}
					})
				} else {
					this.downloadImage()
				}
			},
      downloadImage() {
				imageDownLoad({image_uid: this.swiperList[this.cardCur].uid}).then(res => {
					if (res.code == 1) {
						this.$func.templateSubscribe(res.template_id, res.url ?? '')
						return
					}
					this.$func.showToast(res.msg)
				})
			},
      // cardSwiper
      cardSwiper(e) {
        this.cardCur = e.detail.current
      },
      
      // 弹出压屏窗
      showLandscape() {
        this.openLandscape()
      },
      // 打开压屏窗
      openLandscape() {
        this.show1 = true
      },
      // 关闭压屏窗
      closeLandscape() {
        this.show1 = false
      },
    }
	}
</script>

<style lang="scss" scoped>
  .template-details {
    margin: 0;
    width: 100%;
    height: 100vh;
    color: #fff;
    overflow: hidden;
  }
  /* 胶囊*/
  .tn-custom-nav-bar__back {
    width: 100%;
    height: 100%;
    position: relative;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    box-sizing: border-box;
    background-color: rgba(0, 0, 0, 0.15);
    border-radius: 1000rpx;
    border: 1rpx solid rgba(255, 255, 255, 0.5);
    color: #FFFFFF;
    font-size: 18px;
    
    .icon {
      display: block;
      flex: 1;
      margin: auto;
      text-align: center;
    }
    
    &:before {
      content: " ";
      width: 1rpx;
      height: 110%;
      position: absolute;
      top: 22.5%;
      left: 0;
      right: 0;
      margin: auto;
      transform: scale(0.5);
      transform-origin: 0 0;
      pointer-events: none;
      box-sizing: border-box;
      opacity: 0.7;
      background-color: #FFFFFF;
    }
  }  
  

  
  /* 图标容器15 start */
  .icon15 {
    &__item {
      width: 30%;
      
      border-radius: 10rpx;
      padding: 30rpx;
      margin: 20rpx 10rpx;
      transform: scale(1);
      transition: transform 0.3s linear;
      transform-origin: center center;
      
      &--icon {
        width: 100rpx;
        height: 100rpx;
        font-size: 50rpx;
        border-radius: 50%;
        margin-bottom: 18rpx;
        position: relative;
        z-index: 1;
        
        &::after {
          content: " ";
          position: absolute;
          z-index: -1;
          width: 100%;
          height: 100%;
          left: 0;
          bottom: 0;
          border-radius: inherit;
          opacity: 1;
          transform: scale(1, 1);
          background-size: 100% 100%;
  
            
        }
      }
    }
  }
  
  /* 按钮 */
  .button-1 {
    background-color: rgba(0, 0, 0, 0.15);
    position: fixed;
    /* bottom:200rpx;
      right: 20rpx; */
    top: 25%;
    right: 30rpx;
    z-index: 1001;
    border-radius: 100px;
  }
  .button-2 {
    background-color: rgba(0, 0, 0, 0.15);
    position: fixed;
    /* bottom:200rpx;
      right: 20rpx; */
    top: 35%;
    right: 30rpx;
    z-index: 1001;
    border-radius: 100px;
  }
  .button-3 {
    background-color: rgba(0, 0, 0, 0.15);
    position: fixed;
    /* bottom:200rpx;
      right: 20rpx; */
    top: 45%;
    right: 30rpx;
    z-index: 1001;
    border-radius: 100px;
  }  
  
    

  
  /* 相册 start*/
  .slideshow {
    top: 0;
    position: absolute;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
  }
  
  .slideshow-image {
    position: absolute;
    width: 100%;
    height: 100%;
    background: no-repeat 50% 50%;
    background-size: cover;
    -webkit-animation-name: kenburns;
            animation-name: kenburns;
    -webkit-animation-timing-function: linear;
            animation-timing-function: linear;
    -webkit-animation-iteration-count: infinite;
            animation-iteration-count: infinite;
    -webkit-animation-duration: 16s;
            animation-duration: 16s;
    opacity: 1;
    transform: scale(1.2);
  }
  .slideshow-image:nth-child(1) {
    -webkit-animation-name: kenburns-1;
            animation-name: kenburns-1;
    z-index: 3;
  }
  .slideshow-image:nth-child(2) {
    -webkit-animation-name: kenburns-2;
            animation-name: kenburns-2;
    z-index: 2;
  }
  .slideshow-image:nth-child(3) {
    -webkit-animation-name: kenburns-3;
            animation-name: kenburns-3;
    z-index: 1;
  }
  .slideshow-image:nth-child(4) {
    -webkit-animation-name: kenburns-4;
            animation-name: kenburns-4;
    z-index: 0;
  }
  
  @-webkit-keyframes kenburns-1 {
    0% {
      opacity: 1;
      transform: scale(1.2);
    }
    1.5625% {
      opacity: 1;
    }
    23.4375% {
      opacity: 1;
    }
    26.5625% {
      opacity: 0;
      transform: scale(1);
    }
    100% {
      opacity: 0;
      transform: scale(1.2);
    }
    98.4375% {
      opacity: 0;
      transform: scale(1.2117647059);
    }
    100% {
      opacity: 1;
    }
  }
  
  @keyframes kenburns-1 {
    0% {
      opacity: 1;
      transform: scale(1.2);
    }
    1.5625% {
      opacity: 1;
    }
    23.4375% {
      opacity: 1;
    }
    26.5625% {
      opacity: 0;
      transform: scale(1);
    }
    100% {
      opacity: 0;
      transform: scale(1.2);
    }
    98.4375% {
      opacity: 0;
      transform: scale(1.2117647059);
    }
    100% {
      opacity: 1;
    }
  }
  @-webkit-keyframes kenburns-2 {
    23.4375% {
      opacity: 1;
      transform: scale(1.2);
    }
    26.5625% {
      opacity: 1;
    }
    48.4375% {
      opacity: 1;
    }
    51.5625% {
      opacity: 0;
      transform: scale(1);
    }
    100% {
      opacity: 0;
      transform: scale(1.2);
    }
  }
  @keyframes kenburns-2 {
    23.4375% {
      opacity: 1;
      transform: scale(1.2);
    }
    26.5625% {
      opacity: 1;
    }
    48.4375% {
      opacity: 1;
    }
    51.5625% {
      opacity: 0;
      transform: scale(1);
    }
    100% {
      opacity: 0;
      transform: scale(1.2);
    }
  }
  @-webkit-keyframes kenburns-3 {
    48.4375% {
      opacity: 1;
      transform: scale(1.2);
    }
    51.5625% {
      opacity: 1;
    }
    73.4375% {
      opacity: 1;
    }
    76.5625% {
      opacity: 0;
      transform: scale(1);
    }
    100% {
      opacity: 0;
      transform: scale(1.2);
    }
  }
  @keyframes kenburns-3 {
    48.4375% {
      opacity: 1;
      transform: scale(1.2);
    }
    51.5625% {
      opacity: 1;
    }
    73.4375% {
      opacity: 1;
    }
    76.5625% {
      opacity: 0;
      transform: scale(1);
    }
    100% {
      opacity: 0;
      transform: scale(1.2);
    }
  }
  @-webkit-keyframes kenburns-4 {
    73.4375% {
      opacity: 1;
      transform: scale(1.2);
    }
    76.5625% {
      opacity: 1;
    }
    98.4375% {
      opacity: 1;
    }
    100% {
      opacity: 0;
      transform: scale(1);
    }
  }
  @keyframes kenburns-4 {
    73.4375% {
      opacity: 1;
      transform: scale(1.2);
    }
    76.5625% {
      opacity: 1;
    }
    98.4375% {
      opacity: 1;
    }
    100% {
      opacity: 0;
      transform: scale(1);
    }
  }
    /* 相册 end*/
    
  /* 用户头像 start */
  .logo-image {
    width: 100rpx;
    height: 100rpx;
    position: relative;
  }
  
  .logo-pic {
    background-size: cover;
    background-repeat: no-repeat;
    // background-attachment:fixed;
    background-position: top;
    border: 6rpx solid rgba(255,255,255,0.25);
    box-shadow: 0rpx 0rpx 80rpx 0rpx rgba(0, 0, 0, 0.15);
    border-radius: 50%;
    overflow: hidden;
    // background-color: #FFFFFF;
  }
    
  /* 底部tabbar start*/
  /* 毛玻璃*/
  .dd-glass {
     width: 100%;
     backdrop-filter: blur(20rpx);
    -webkit-backdrop-filter: blur(20rpx);
  }
  
  .footerfixed{
   position: fixed;
   // margin: 20rpx;
   margin: 40rpx 5%;
   width: 90%;
   bottom: calc(env(safe-area-inset-bottom) / 2);;
   z-index: 999;
   background-color: rgba(0, 0, 0, 0.15);
   box-shadow: 0rpx 0rpx 30rpx 0rpx rgba(0, 0, 0, 0.07);
  }
  
  .tabbar {
    display: flex;
    align-items: center;
    min-height: 110rpx;
    justify-content: space-between;
  	padding: 0;
  	height: calc(110rpx + env(safe-area-inset-bottom) / 2);
  	// padding-bottom: calc(env(safe-area-inset-bottom) / 2);
  }
  
  .tabbar .action {
  	font-size: 22rpx;
  	position: relative;
  	flex: 1;
  	text-align: center;
  	padding: 0;
  	display: block;
  	height: auto;
  	line-height: 1;
  	margin: 0;
  	overflow: initial;
  }
  
  .tabbar .action .bar-icon {
  	width: 100rpx;
  	position: relative;
  	display: block;
  	height: auto;
  	margin: 0 auto 10rpx;
  	text-align: center;
  	font-size: 42rpx;
  }
  
  .tabbar .action .bar-icon image {
  	width: 50rpx;
  	height: 50rpx;
  	display: inline-block;
  }  
  
  
  /* 全屏轮播  start*/
  .card-swiper {
    height: 100vh !important;
  }
    
  .card-swiper swiper-item {
    width: 750rpx !important;
    left: 0rpx;
    box-sizing: border-box;
    overflow: initial;
  }
    
  .card-swiper swiper-item .swiper-item {
    width: 100%;
    display: block;
    height: 100vh;
    border-radius: 0rpx;
    transform: scale(0.9);
    transition: all 0.2s ease-in 0s;
    will-change: transform;
    overflow: hidden;
  }
    
  .card-swiper swiper-item.cur .swiper-item {
    transform: scale(1);
    transition: all 0.2s ease-in 0s;
    will-change: transform;
  }
    
  .image-banner{
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .image-banner image{
    width: 100%;
    // height: 100%;
  }
  
  /* 轮播指示点 start*/
  .indication{
    z-index: 9999;
    width: 100%;
    height: 36rpx;
    position: fixed;
    display:flex;
    flex-direction:row;
    align-items:center;
    justify-content:center;
  }
  
  .spot{
    background-color: #FFFFFF;
    opacity: 0.6;
    width: 10rpx;
    height: 10rpx;
    border-radius: 20rpx;
    top: calc(-280rpx - env(safe-area-inset-bottom) / 2);
    top: calc(-280rpx - constant(safe-area-inset-bottom));
    margin: 0 8rpx !important;
    position: relative;
  }
  
  .spot.active{
    opacity: 1;
    width: 30rpx;
    background-color: #FFFFFF;
  }
</style>
