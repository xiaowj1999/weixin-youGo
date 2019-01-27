<template>
  <div class="index-container">
      <div class="header-search">
        <input type="search" placeholder="搜索">
        <icon type="search" size="32rpx"></icon>
      </div>
      <!-- 轮播图区域 -->
      <swiper
          indicator-dots
          autoplay
          circular
          class="swiper-container"
        >
        <swiper-item v-for="item in swiperList" :key="item.image_src">
          <img :src="item.image_src" />
        </swiper-item>
      </swiper>
    <!-- 分类导航区域 -->
      <ul class="nav-container">
        <li v-for="item in navCategoryList" :key="item.image_src">
          <a href="#">
            <img :src="item.image_src" alt="">
            <p>{{item.name}}</p>
          </a>
        </li>
      </ul>
      <!--楼层区域 -->
      <div class="floor-container">
        <div class="floor" v-for="item in floordata">
            <!-- 顶部 -->
            <div class="floor-title">
              <img :src="item.floor_title.image_src">
              <h3>{{item.floor_title.name}}</h3>
            </div>
          <!-- 内容 -->
          <div class="floor-content">
            <img v-for="(it, i) in item.product_list" :src="it.image_src" />
          </div>
        </div>
      </div>
      <!-- 底部区域 -->
      <div class="footer">
          <i class="iconfont icon-xiao"></i>
          <span>我是有底线的</span>
      </div>
  </div>
</template>

<script>
import wxios from "../../utils/index.js"

export default {
  data() {
    return {
      swiperList:[],
      //导航分类数据
      navCategoryList:[],
      //获取楼层数据
      floordata:[]
    }
  },
  async onLoad() {
    //获取轮播图的数据
    let swiperRes = await wxios.get({
      url:"api/public/v1/home/swiperdata"
    })
    this.swiperList = swiperRes.data.message
    //获取导航栏分类的数据
    let navRes = await wxios.get({
      url:"api/public/v1/home/catitems"
    })
    // console.log(navRes);
    this.navCategoryList = navRes.data.message
    //获取楼层数据
    let floorRes = await wxios.get({
      url:"api/public/v1/home/floordata"
    })
    // console.log(floorRes);
    this.floordata = floorRes.data.message
    
  },
}
</script>

<style lang="scss">
$mainColor:#eb4450;
.index-container {
  padding-top: 100rpx;
}
.header-search {
  z-index: 999;
  width: 100%;
  background-color:$mainColor;
  padding: 20rpx 16rpx;
  box-sizing: border-box;
  position:fixed;
  top: 0;
  left: 0;
  height: 100rpx;
  input {
    display: block;
    width: 100%;
    height: 60rpx;
    background-color: #fff;
    border-radius: 10rpx;
    padding-left: 382rpx;
    box-sizing: border-box;
    font-size: 24rpx;
  }
  icon {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
  }

}
.swiper-container {
  width: 100%;
  height: 340rpx;
  img {
    display: block;
    width: 100%;
    height: 100%;
  }
}
.nav-container {
  display: flex;
  padding: 29rpx 32rpx;
  li {
    flex: 1;
    a {
      display: block;
      width: 100%;
      height: 100%;
      img{
      width: 128rpx;
      height: 128rpx;
      display: block;
      margin: 0 auto;
      
    }
    p {
      margin-top: 16rpx;
      font-size: 22rpx;
      text-align: center;
    }
    }
  }
}
.floor-container {
  .floor-title {
    padding:30rpx 0 30rpx 15rpx;
    box-sizing:border-box;
    height: 90rpx;
    position: relative;
    h3{
      color: #ff7b94;
      font-size: 36rpx;
      position: absolute;
      top: 50%;
      left: 30rpx;
      transform: translateY(-50%);
    }
    img {
      width: 100%;
      display: block;
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
    }
  }
  .floor-content {
    padding: 20rpx 0 0 16rpx;
    overflow: hidden;
    img {
      display: block;
      width: 33.33%;
      float: left;
      width: 230rpx;
      height: 190rpx;
      margin-right: 15rpx;
      &:first-child {
        widows: 230rpx;
        height: 390rpx;
      }
      &:nth-child(2){
        margin-bottom: 10rpx;
      }
      &:nth-child(3){
        margin-bottom: 10rpx;
      }
    }
  }
}
.footer {
  height: 231rpx;
  width: 100%;
  background-color: #f4f4f4;
  text-align: center;
  color: #999999;
  font-size: 30rpx;
  padding-top: 22rpx;
  i {
    display: inline-block;
    padding-right: 14rpx;
  }
}

</style>
