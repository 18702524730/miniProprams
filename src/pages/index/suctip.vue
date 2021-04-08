<template>
    <div class="resultboxs">
        <div class="comhead"><span class="back" @click="toback"></span> 链科</div>
        <div class="tphone" >
            <div class="msgs">
                <div class="guwen">拨打电话进行1对1咨询</div>
                <div class="tit">咨询顾问：饶老师</div>
                <div class="zixun" @tap="dalphone">
                    <span class="iconphone"></span>
                    <span>立即咨询</span>
                </div>
            </div>
            <div class="headpic">

            </div>
        </div>
        <div class="contboxres">
            <div class="successbox"></div>
            <div class="tips">
                <p>您的申报辅导请求我们已经收到</p>
                <p>1个工作日内申报专家将与您取得联系</p>
            </div>
            <div class="backresult" @click="toback">
                返回评估结果
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
        }
    },
    methods:{
        toback(){
            this.$router.go(-1)
        },
        async getPhoneNumber(e) {
            // this.tosuc()
            let ss = await this.API.interfaces.checkLogin()
            if(e.mp.detail.encryptedData){
                let phone = await this.API.interfaces.getPhoneNumber(e,this.companyName);
                this.tosuc()
            }else{
                wx.showToast({
                    title:'请授权手机号，领取上门辅导',
                    icon:'none',
                    duration: 2000
                })
            }
        },
        dalphone(){
            wx.makePhoneCall({
                phoneNumber: '15868120211'
            })
        }
    }
}
</script>
<style lang="scss">
.resultboxs{
    min-height: 100%;
    background-color: #fff;
    padding-bottom: 100px;
    padding-top: 170px;
    .contboxres{
        padding: 112px 40px 100px;
        margin-top: -270px;
        background-color: #fff;
    }
    .pdbox{
        padding: 0 40px;
    }
    .comhead{
        position: fixed;
        top:0;
        left:0;
        z-index: 99;
        width: 100%;
        height: 170px;
        background-color: #247DFF;
        text-align: center;
        padding-top: 96px;
        font-size:34px;
        font-family:PingFangSC-Medium,PingFang SC;
        font-weight:500;
        color:rgba(255,255,255,1);
        line-height:44px;
        .back{
            position: absolute;
            left: 40px;
            top: 100px;
            width: 20px;
            height: 36px;
            background: url(~assets/img/homepage/left.png) center center;
            background-size: 100% 100%;
        }
    }
    .tphone{
        width:100%;
        height:480px;
        // padding: 24px 40px;
        background:linear-gradient(180deg,rgba(36,125,255,1) 0%,#EFF1F8 100%);
        .msgs{
            float: left;
            width: 450px;
            padding-left: 60px;
            margin-right: 50px;
        }
        .zixun{
            height: 68px;
            width: 212px;
            padding: 16px 0;
            background:linear-gradient(270deg,rgba(99,128,255,1) 0%,rgba(18,98,215,1) 100%);
            border-radius: 34px;
            text-align: center;
            line-height: 36px;
            font-size: 28px;
            color:#fff;
            >span{
                vertical-align: middle;
            }
        }
        .headpic{
            float: left;
            width: 190px;
            height: 190px;
            background: url(~assets/img/homepage/ls.png) center center no-repeat;
            background-size: 100% 100%;
            border-radius: 50%;
        }
        .iconphone{
            display: inline-block;
            width: 20px;
            height: 20px;
            background: url('~assets/img/icon/phonet.png') center center no-repeat;
            background-size: 100% 100%;
            margin-right: 10px;
            // background-color: #379dea;
        }
        .guwen{
            color:#fff;
            height:50px;
            font-size:36px;
            font-family:PingFangSC-Medium,PingFang SC;
            font-weight:500;
            line-height:50px;
        }
        .tit{
            color:#fff;
            width:192px;
            height:36px;
            font-size:24px;
            font-family:PingFangSC-Regular,PingFang SC;
            line-height:36px;
            margin-bottom: 24px;
        }
    }
    .tips{
        text-align: center;
        font-size:28px;
        font-weight:400;
        color:rgba(51,51,51,1);
        line-height:40px;
        margin-bottom: 106px;
        p{
            text-align: center;
        }
    }
    
    .successbox{
        width: 102px;
        height: 102px;
        background: url('~assets/img/icon/suc.png') center center no-repeat;
        background-size: 100%;
        margin: 0 auto 43px;
    }
    .backresult{
        height:90px;
        background:rgba(47,128,246,1);
        border-radius:6px;
        width:100%;
        color:#fff;
        font-size:32px;
        font-weight:400;
        line-height:90px;
        text-align: center;
    }
}
</style>
