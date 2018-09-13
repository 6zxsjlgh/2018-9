<template>
  <div>
    <!-- 顶部 -->
    <myheader></myheader>
   <!-- 内容区域 -->
   <div class="left">
       <scroll-view scroll-y style="height: 200px;" bindscrolltoupper="upper">
          <div class="item">
              
          </div>
  </scroll-view>

   </div>
   <div class="right"></div>
  </div>
</template>

<script>
import myheader from "@/components/header"
import tool from "../../utils/index.js"
import { SEMVER_SPEC_VERSION } from 'semver/index.js';
export default {
  data:function () {
  return{
   
  }
    },
  components:{
    myheader
  },
  // 内容 
  onLoad(){
     console.log("二页面")
    // tool.thenAjax({
    //   url:"api/public/v1/categories",
    // }).then(res=>{
    //   console.log(res);
    // })
  }
}

</script>

<style lang="less">

</style>
