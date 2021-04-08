<template>
    <div class="kejipingce">
        <div class="comhead"><span class="back" @click="toback"></span> 链科</div>
        <div class="compbg"></div>
        <div class="pdbox">
            <!-- <h3 class="typetitle">科技项目评测</h3> -->
            <div class="labnames">企业名称：</div>
            <div class="textbox"><input type="text" v-model="companyName" placeholder="请输入您的企业全称"></div>
            <div class="labnames">您企业是否认定为国家高新技术企业？</div>
            <div class="radiobox">
                <radio-group @change="changetype">
                <label class="space"><radio value="1" :checked="isNewHigh==1">是</radio></label>
                <radio value="2" :checked="isNewHigh==2">否</radio>
                </radio-group>
            </div>
            <div class="nextstep" @click="tonext">下一步</div>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            companyName:'',
            isNewHigh: '',
            savedata:{},
            registerTime:''
        }
    },
    onShow(){
        // this.fromtype = this.$root.$mp.query.home;
        let ret = wx.getStorageSync('companydata')
        if(ret){
            this.savedata =JSON.parse(ret);
            this.companyName=this.savedata.companyName;
            this.isNewHigh= this.savedata.isNewHigh-0;
        }else{
            this.companyName='';
            this.isNewHigh=''
        }
    },
    methods:{
        toback(){
            this.$router.go(-1)
        },
        async gettime(){
            let data = {
                companyName: this.companyName,
                isNewHigh: this.isNewHigh
            }
            try {
                let res = await this.API.home.gettime(data);
                this.registerTime = res.registerTime
                let sdata = {
                    companyName: this.companyName,
                    isNewHigh: this.isNewHigh,
                    registerTime: this.registerTime
                }
                let str = JSON.stringify(sdata);
                wx.setStorageSync('companydata',str);
                this.$router.push({path:'/pages/index/ceping'})
            } catch (error) {
                wx.showToast({
                    title: error.response.data.msg||'获取企业注册时间失败',        // 显示文本
                    icon:'none',          // 图标类型
                    duration:  2000,        // 关闭时间
                })
            }
            
            // if(this.isNewHigh==2){
            //     this.nowtype = 3
                
            // }
            // if(this.isNewHigh==1){
            //     this.nowtype = 2;
                
            // }
            // console.log(res)
        },
        changetype(e){
            this.isNewHigh = e.target.value
            
        },
        tonext(){
            if(!this.companyName){
                wx.showToast({
                    title: '请填写企业名称',        // 显示文本
                    icon:'none',          // 图标类型
                    duration:  2000,        // 关闭时间
                })
                return false
            }
            if(!this.isNewHigh){
                wx.showToast({
                    title: '请是否是高新企业',        // 显示文本
                    icon:'none',          // 图标类型
                    duration:  2000,        // 关闭时间
                })
                return false
            }
            this.gettime()
        }
    },
}
</script>

<style lang="scss">
.kejipingce{
    min-height: 100%;
    background-color: #fff;
    padding-top: 170px;
    font-family:'PingFangSC-Medium','PingFang SC';
    .datepicker{
        height: 60px;
        padding: 10px;
        border-radius: 4px;
        margin-bottom: 70px;
        border: 1px solid #e5e5e5;
        .picker{
            color:#333;
            .tishi{
                color:#B0B0B0;
            }
        }
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
    .pdbox{
        padding: 0 40px;
    }
    .compbg{
        height: 475px;
        background: url(~assets/img/homepage/bg.png) no-repeat center bottom;
        background-size: 100% auto;
        margin-bottom: 40px;
    }
    .typetitle{
        height:50px;
        font-size:36px;
        font-weight:500;
        color:rgba(36,125,255,1);
        line-height:50px;
        margin-bottom: 16px;
        span{
            float: left;
            margin-right: 10px;
        }
        .gaoxin{
            padding: 0 10px;
            height: 34px;
            margin-top: 8px;
            line-height: 34px;
            background-color: #247DFF;
            color: #fff;
            font-weight: normal;
            font-size: 24px;
            vertical-align: bottom
        }
    }
    .labname{
        height:40px;
        font-size:28px;
        font-weight:400;
        color:#247DFF;
        line-height:40px;
        margin-bottom: 16px;
        padding-left: 10px;
        border-left: 10px solid #247DFF;
    }
    .labnames{
        height:40px;
        font-size:28px;
        font-weight:400;
        color:#333;
        line-height:40px;
        margin-bottom: 16px;
    }
    .textbox{
        height: 82px;
        padding: 20px;
        border: 1px solid #E5E5E5;
        margin-bottom: 32px;
        color:#247DFF;
    }
    .radiobox{
        padding: 16px 0;
        margin-bottom: 102px;
        label{
            margin-right: 200px;
        }
        .itemblock{
            margin-bottom: 28px;
        }
    }
    .nextstep{
        width: 670px;
        height:90px;
        margin: 0 auto;
        background:rgba(47,128,246,1);
        border-radius:6px;
        color:#fff;
        font-size:32px;
        font-weight:400;
        line-height:90px;
        text-align: center;
    }
    .mt200{
        margin-top: 200px;
    }
    .mt16{
        margin-top: 16px;
    }
    
}
</style>
