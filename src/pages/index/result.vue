<template>
    <div class="resultbox">
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
        
        <div class="contbox" v-if="pinggu==1">
            <div v-if="result.length" class="listdatabox">
                <h3 class="cname">{{companyName}}</h3>
                <h3 class="gongxi">恭喜，您获可申报以下项目：</h3>
                <ul class="resultlist">
                    <li v-for="(item,index) in result" :key="index"><span class="title">{{item.type}} </span><span class="sanjiao"></span><span class="jine">{{item.money}}</span></li>
                </ul>
            </div>
            <div v-if="!result.length" class="nodatabox">
                <div class="nodata"></div>
                <p>抱歉！暂无可申报项目</p>
                <p>建议您拨打咨询专线了解详情</p>
            </div>
            <div class="pdbox">
                <div class="getphonenum">
                    <button  open-type="getPhoneNumber" @getphonenumber="getPhoneNumber" >立刻上门申报辅导</button>
                </div>
                <div class="shuoming">系统将向您申请获取手机号，请同意以便为您提供服务</div>
                <div class="chongxin" @click="back">
                    我想重新评估
                </div>
            </div>
        </div>
        <div v-if="pinggu==2" class="contboxres">
            <div class="nodatabox">
                <div class="successbox"></div>
                <div class="tips">
                    <p>您的申报辅导请求我们已经收到</p>
                    <p>1个工作日内申报专家将与您取得联系</p>
                </div>
            </div>
            <div class="pdbox">
                <div class="backresult" @click="pinggu=1">
                    返回评估结果
                </div>
                <div class="shuoming">系统将向您申请获取手机号，请同意以便为您提供服务</div>
                <div class="chongxin" @click="back">
                    我想重新评估
                </div>
            </div>
            <!-- <div class="backresult" @click="pinggu=1">
                返回评估结果
            </div> -->
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            pinggu:1,
            result:[
                // {type:'市级高新技术企业研究开发中心',money:'202万'},
                // {type:'市级高新技术企业研究开发中心',money:'202万'}
            ],
            companyName:''
        }
    },
    onShow(){
        this.pinggu = 1;
        let rets = wx.getStorageSync('companydata')
        let cdatas = JSON.parse(rets)
        this.companyName=cdatas.companyName;
        let list = wx.getStorageSync('cepingresult');
        this.result = JSON.parse(list);
    },
    methods:{
        toback(){

            this.$router.go(-1)
            this.pinggu = 1;
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
        back(){
            // this.$router.replace({path:'/pages/index/ceping?home=2'})
            this.$router.go(-1)
        },
        tosuc(){
            this.pinggu = 2
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
.resultbox{
    min-height: 100%;
    background-color: #EFF1F8;
    padding-bottom: 100px;
    padding-top: 168px;
    .contbox{
        margin-top: -270px;
    }
    .contboxres{
        margin-top: -270px;
    }
    .pdbox{
        padding: 0 40px;
    }
    .comhead{
        position: fixed;
        top:0;
        left:0;
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
        height:484px;
        padding-top: 4px;
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
    .cname{
        height:36px;
        font-size:26px;
        font-family:PingFangSC-Regular,PingFang SC;
        font-weight:400;
        color:rgba(36,125,255,1);
        line-height:36px;
        margin-bottom: 10px;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
    }
    .gongxi{
        height:50px;
        font-size:36px;
        font-family:PingFangSC-Regular,PingFang SC;
        color:rgba(51,51,51,1);
        line-height:50px;
        margin-bottom: 36px;
    }
    .resultlist{
        >li{
            height: 72px;
            margin-bottom: 24px;
            span{
                vertical-align: middle;
            }
            .title{
                float: left;
                padding-left: 30px;
                width: 468px;
                height:72px;
                background:linear-gradient(270deg,rgba(141,185,252,1) 0%,rgba(36,125,255,1) 100%);
                line-height: 72px;
                font-size: 30px;
                color: #fff;
                
                
            }
            .sanjiao{
                    float: left;
                    width:0;
                    height: 0;
                    border-width: 36px;
                    // margin-right: 30px;
                    border-style: dashed dashed dashed solid;
                    border-color: transparent transparent transparent #8DB9FC;
                }
            .jine{
                float: left;
                width:120px;
                height:60px;
                font-size:42px;
                font-family:PingFangSC-Medium,PingFang SC;
                font-weight:500;
                color:rgba(198,45,0,1);
                line-height:60px;
            }
        }
    }
    .getphonenum{
        height:90px;
        background:rgba(47,128,246,1);
        border-radius:6px;
        width:100%;
        margin-bottom: 16px;
        button{
            border:none;
            outline: none;
            background: none;
            float: left;
            width: 100%;
            height: 100%;
            margin: 0;
            padding:0;
            color:#fff;
            font-size:32px;
            font-weight:400;
            line-height:90px; 
            text-align: center;
        }
    }
    .shuoming{
        width:100%;
        height:33px;
        margin-bottom: 16px;
        font-size:24px;
        font-family:PingFangSC-Regular,PingFang SC;
        font-weight:400;
        color:rgba(176,176,176,1);
        line-height:33px;
        text-align: center;
    }
    .chongxin{
        width:100%;
        text-align: center;
        height:90px;
        border-radius:6px;
        border:1px solid rgba(47,128,246,1);
        font-size:32px;
        font-family:'PingFangSC-Regular','PingFang SC';
        font-weight:400;
        color:rgba(36,125,255,1);
        line-height:90px;
    }
    .successbox{
        width: 102px;
        height: 102px;
        background: url('~assets/img/icon/suc.png') center center no-repeat;
        background-size: 100%;
        margin: 30px auto 42px;
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
    .listdatabox{
        width: 720px;
        margin: 0 auto 60px;
        padding:36px 28px;
        background-color: #fff;
        border-radius: 14px;
    }
    .nodatabox{
        width: 720px;
        margin: 0 auto 90px;
        padding-top: 114px;
        height: 516px;
        text-align: center;
        background-color: #fff;
        border-radius: 14px;
        .nodata{
            margin: 0 auto 30px;
            width: 282px;
            height: 220px;
            background: url('~assets/img/homepage/nodata.png') center center no-repeat;
            background-size: 100% 100%;
        }
        >p{
            font-size:24px;
            font-family:PingFangSC-Regular,PingFang SC;
            color:rgba(176,176,176,1);
            line-height:36px;
        }
    }
}
</style>
