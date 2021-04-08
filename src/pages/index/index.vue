<template>
  <div class="firstpage">
    <div class="comhead">链科</div>
    <div class="topbg"></div>
    
    <div @click="tocp" class="cepingbtn">立即评测</div>
    <div class="jgbox"></div>
    <p>长三角（杭州·江干）科技大市场版权所有</p>
    <p>指导单位：杭州市江干区科学技术局</p>
  </div>
</template>
<script>
export default {
  data(){
    return{
    }
  },
  // 监听用户点击页面内转发按钮
  // onShareAppMessage() {
  //   let obj = {};
  //   let memberId = this.$storage.get('auth').member_id;
  //   obj = {
  //     title: '链科，链接每一个企业的科技价值！',
  //     path: "/pages/index/index?memberId="+ memberId,
  //     //imageUrl: 'https://www.ipsebe.com/cms/webfile/upload/2018/12-14/18-06-0608961222801360.jpg'
  //   }
  //   return obj;
  // },
  methods:{
    tocp(){
      wx.setStorageSync('companydata',null)
      wx.setStorageSync('savelocaldata',null)
      this.$router.push({path:'/pages/index/company'})
    }
  }
}
</script>
<style lang="scss">
.firstpage{
  min-width: 100%;
  min-height: 100%;
  background-color: #fff;
  .topbg{
    height: 810px;
    background: url(~assets/img/homepage/bga.png) no-repeat left top;
    background-size: 100% 100%;
    margin-bottom: 94px;
  }
  .comhead{
        position: fixed;
        top:0;
        left:0;
        z-index: 99;
        width: 100%;
        height: 170px;
        text-align: center;
        padding-top: 96px;
        font-size:34px;
        font-family:PingFangSC-Medium,PingFang SC;
        font-weight:500;
        color:rgba(255,255,255,1);
        line-height:44px;
    }
  .cepingbtn{
    width:486px;
    height:120px;
    margin: 0 auto 66px;
    background:linear-gradient(270deg,rgba(131,203,255,1) 0%,rgba(98,162,255,1) 100%);
    border-radius:60px;
    text-align: center;
    line-height: 120px;
    font-size: 36px;
    font-weight:500;
    color:rgba(255,255,255,1);
  }
  .jgbox{
    width: 126px;
    height: 96px;
    margin: 0 auto 36px;
    background: url(~assets/img/homepage/jg.png) no-repeat center center;
    background-size: auto 100%;
  }
  >p{
    height:28px;
    font-size:20px;
    font-family:PingFangSC-Regular,PingFang SC;
    color:rgba(51,51,51,1);
    line-height:28px;
    text-align: center;
    margin-bottom: 8px;
  }
  // .bottombox{
  //   position: absolute;
  //   bottom: 60px;
  //   width: 100%;
  //   left:0;
  //   text-align: center;
  // }
}
</style>

