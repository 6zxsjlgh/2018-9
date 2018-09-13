<template>
  <div>
       <myheader></myheader>

    <swiper indicator-dots indicator-active-color="#fff" autoplay interval="3000" >
        <swiper-item v-for="item in switthc " :key="item.name">
           <image mode="aspectFill"  :src="item.image_src"></image>
      </swiper-item>
    </swiper>
    <ul class="box-back">
       <li class="backaa" v-for="item in imga" :key="item.name">
         <img class="img" :src="item.image_src" alt="">
          <span class="span">{{item.name}}</span>
       </li>
    </ul>


    <!-- 楼层 -->
   <div class="box-titl" v-for="(item, index) in titledada" :key="index">
     <div class="title">
      <text class="text">{{item.floor_title.name}}</text>
      <img class="img" :src="item.floor_title.image_src" alt="">
      </div>
      <div class="concen" >
        <a class="nav" v-for="(it, i) in item.product_list" :key="i" href="">
        <img :src="it.image_src" alt="">
        </a>
      </div>
   </div>
   <!-- 我是有底线的 -->
  <div class="listxin"> 
    <span class="iconfont icon-xiao"></span>到底了
  </div>
  <!-- 返回顶部 -->
  <div class="to-top" @click="dqec" v-show="isshow">
    <span class="iconfont icon-jiantoushang"></span>
    顶部
  </div>

  </div>
</template>

<script>
import tool from "../../utils/index.js";
import myheader from "@/components/header"
console.log(tool);
export default {
  data: function() {
    return {
      //轮播图
      switthc:[],
      //分类
      imga:[],
      //// 楼层
    titledada:[],
    //回到顶部
    isshow:false
    };
  },
  onLoad() {
    tool.thenAjax({
       url:"api/public/v1/home/swiperdata"
    }).then(res=>{
     this.switthc=res.data.message
      return tool.thenAjax({
        url:"api/public/v1/home/catitems"
      })
    }).then(res=>{
     this.imga=res.data.message;
     return tool.thenAjax({
      url:"api/public/v1/home/floordata"                   //楼层数据 
     }).then(res=>{
      this.titledada=res.data.message;
     })
    })
  },
  components:{
    myheader
  },
  onPageScroll(eveng){
   if(eveng.scrollTop>190){
       this.isshow=true;
   }else{
       this.isshow=false;
   }
  },


  methods:{
    dqec(){
     wx.pageScrollTo({
       scrollTop:0,
       duration:300
     })
    }
  }

};
</script>

<style lang='less'>
swiper{
  height: 384rpx;
   margin-top: -1rpx;
  swiper-item{
    image{
      width: 100%;
      height: 100%;
      display: block;
    }
  }
}
//分类部份
.box-back{
  padding-top:20rpx;
  padding-bottom: 20rpx;
  display: flex;
  .backaa{
    flex: 1;
    .img{
      width: 100rpx;
      height: 100rpx;
      display: block;
      margin: 0 auto;
    }
    .span{
      display: block;
      text-align: center;
      color: #bbb;
    }
  }
}

// 楼层
.box-titl{
   .title{
     position: relative;
     .text{
       position: absolute;
       left: 20rpx;
       top: 10rpx;
       font-size: 50rpx;
       color: #ff2d4a;
       font-weight: 700;
      text-align: center;
     }
     .img{
       height: 85rpx;
       width: 100%;
     }
   }
   .concen{
     padding: 20rpx 16rpx;
        height: 440rpx;
      .nav{
        height: 100%;
        width: 33.33%;
        display: block;
        float: left;
        box-sizing: border-box;
        padding: 5rpx;
      }
      img{
        width: 100%;
        height: 100%;
        display: block;
      }
      .nav:not(:first-child){
        height:50%;
      }
   }
}
.listxin{
      height: 130rpx;
      background-color: #fff;
      text-align: center;
      line-height: 130rpx;
      font-size: 30rpx;
      color: #ccc;
      display: block;
    .iconfont{
    }
}
.to-top{
    width: 80rpx;
    height: 80rpx;
    position: fixed;
    bottom: 90rpx;
    right: 20rpx;
   text-align: center;
   background-color:azure;
   border: 2rpx solid #333;
  font-size: 26rpx;
  color: #000;
  border-radius: 50%;
  .iconfont{
   display: block;
  }
}



</style>
