<template>
  <view class="page-c">
    
    <!-- 顶部自定义导航 -->
    <tn-nav-bar :isBack="false" :bottomShadow="false" backgroundColor="none">
      <view class="custom-nav tn-flex tn-flex-col-center tn-flex-row-left" @click="tn('/minePages/message')">
        <view class="custom-nav__back">
          <text class="tn-text-bold tn-text-xl tn-color-black">每日精选</text>
        </view>
      </view>
    </tn-nav-bar>
    
    <!-- 卡片轮播，图片均为凶姐本人照片，请勿将图片用于奇奇怪怪的地方，谢谢大佬们-->
    <view class="swiper tn-margin-left tn-margin-right" style="height:89vh" :style="{paddingTop: vuex_custom_bar_height + 10 +'px'}" @click="tn('/pageA/details/details')">
      <tn-stack-swiper :list="list" direction="vertical" height="105%" :switchRate="20" :scaleRate="0.05" :translateRate="7.2"></tn-stack-swiper>
    </view>
    
    <!-- 两个按钮，有需要直接显示出来即可-->
    <!-- <view class="tn-footerfixed">
      <view class="tn-flex">
        <view class="tn-flex-1 tn-padding-sm tn-radius justify-content-item" @click="tn('')">
          <view class="tn-flex tn-flex-direction-column tn-flex-row-center tn-flex-col-center">
            <view class="icon4__item--icon tn-flex tn-flex-row-center tn-flex-col-center tn-shadow-blur">
              <view class="tn-icon-like-lack tn-cool-color-icon4 tn-bg-blue"></view>
            </view>  
            <view class="tn-color-gray--dark tn-text-center">
              <text class="tn-text-ellipsis tn-text-sm">收 藏</text>
            </view>
          </view>
        </view>
        <view class="tn-flex-1 tn-padding-sm tn-radius justify-content-item" @click="tn('')">
          <view class="tn-flex tn-flex-direction-column tn-flex-row-center tn-flex-col-center">
            <view class="icon4__item--icon tn-flex tn-flex-row-center tn-flex-col-center tn-shadow-blur">
              <view class="tn-icon-download tn-cool-color-icon4 tn-bg-purplered"></view>
            </view>  
            <view class="tn-color-gray--dark tn-text-center">
              <text class="tn-text-ellipsis tn-text-sm">下 载</text>
            </view>
          </view>
        </view>
      </view>
    </view> -->
    
    
    <!-- <view class='tn-tabbar-height'></view> -->
    
  </view>
</template>

<script>
	import { imageItemList } from '@/utils/api/image'
  export default {
    name: 'PagesC',
  	data() {
  	  return {
  	    imageUid: '483316112570716083',
  	    list: [],
  	    autoplay: false
  	  }
  	},
  	onReady() {
  	  this.$nextTick(() => {
  	    this.initSwiperContainer()
  	  })
  	},
  	onShow() {
  	  this.autoplay = true
  	},
		created() {
			this.getImageList()
		},
  	onHide() {
  	  this.autoplay = false
  	},
  	methods: {
			getImageList() {
				imageItemList({image_uid: this.imageUid}).then(res => {
					for (let i = 0; i < res.items.length; i++) {
						this.list.push({
								image: (res.items[i].url + res.items[i].path)
							})
					}
				})
			},
      // 跳转
      tn(e) {
        uni.navigateTo({
          url: e + "?image_uid=" + this.imageUid,
        });
      },
  	  // 初始化轮播图容器
  	  initSwiperContainer() {
  	    // 获取底部tabbar信息
  	    this._tGetRect('.tabbar').then((res) => {
  	      if (!res.height) {
  	        setTimeout(() => {
  	          this.initSwiperContainer()
  	        }, 10)
  	        return
  	      }
  	      // 获取系统信息
  	      const systemInfo = uni.getSystemInfoSync()
  	      this.swiperContainerHeight = systemInfo.safeArea.height - res.height - 10
  	    })
  	  }
  	}
  }
</script>

<style lang="scss" scoped>
  .page-c {
    max-height: 100vh;
    }
    
  /* 自定义导航栏内容 start */
  .custom-nav {
    height: 100%;
    
    &__back {
      margin: auto 30rpx;
      font-size: 40rpx;
      margin-right: 10rpx;
      flex-basis: 5%;
      width: 100rpx;
      position: absolute;
    }
  }
  /* 自定义导航栏内容 end */
  
  /* 底部安全边距 start*/
  .tn-tabbar-height {
  	min-height: 120rpx;
  	height: calc(140rpx + env(safe-area-inset-bottom) / 2);
    height: calc(140rpx + constant(safe-area-inset-bottom));
  }
  
  /* 卡片轮播图 start */
  .swiper {
    border-radius: 10rpx;
    overflow: hidden;
  }
  /* 轮播图 end */
  
  /* 底部固定按钮*/
  .tn-footerfixed {
    position: fixed;
    width: 100%;
    bottom: calc(130rpx + env(safe-area-inset-bottom));
    z-index: 1024;
  }
  
/* 图标容器4 start */
  .tn-cool-color-icon4{
    // background-image: -webkit-linear-gradient(135deg, #ED1C24, #FECE12);
    // background-image: linear-gradient(135deg, #ED1C24, #FECE12);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    text-fill-color: transparent;
  }
  .icon4 {
    &__item {
      width: 30%;
      background-color: #FFFFFF;
      border-radius: 10rpx;
      padding: 30rpx;
      margin: 20rpx 10rpx;
      transform: scale(1);
      transition: transform 0.3s linear;
      transform-origin: center center;
      
      &--icon {
        width: 110rpx;
        height: 110rpx;
        font-size: 55rpx;
        border-radius: 50%;
        margin-bottom: 18rpx;
        position: relative;
        z-index: 1;
        background-color: rgba(255,255,255,0.8);
        backdrop-filter: blur(20rpx);
        -webkit-backdrop-filter: blur(20rpx);
        box-shadow: 0rpx 0rpx 30rpx 0rpx rgba(0, 0, 0, 0.07);
      }
    }
  }    
    
</style>