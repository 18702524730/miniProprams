<template>
    <div class="kejipingce">
        <div class="comhead"><span class="back" @click="toback"></span> 链科</div>
        <div v-if="nowtype==1" class="pdbox">
            <h3 class="typetitle"><span>{{companyName}}</span> <span class="gaoxin">高新</span></h3>
            <div class="labname" v-if="showtime">企业注册时间</div>
            <div class="datepicker" v-if="showtime">
                <picker mode="date" :value="date" start="1900-01-01" end="2020-12-31" @change="bindDateChange" >
                    <view class="picker">
                    <span v-if="!date" class="tishi">请选择注册时间</span> {{date}}
                    </view>
                </picker>
            </div>
            <div class="labname">上年度销售收入(万元)</div>
            <div class="radiobox">
                <radio-group @change="changetypea">
                <div class="itemblock"><radio value="1" :checked="lastYearSalesRevenue==1">小于3000</radio></div>
                <div class="itemblock"><radio value="2" :checked="lastYearSalesRevenue==2">3000~8000</radio></div>
                <div class="itemblock"><radio value="3" :checked="lastYearSalesRevenue==3">8000~2亿</radio></div>
                <div class="itemblock"><radio value="4" :checked="lastYearSalesRevenue==4">大于2亿</radio></div>
                </radio-group>
            </div>
            <div class="labname">科研载体</div>
            <div class="radiobox">
                <radio-group @change="changetypeb">
                <div class="itemblock"><radio value="1" :checked="researchCarrier==1">无</radio></div>
                <div class="itemblock"><radio value="2" :checked="researchCarrier==2">市级</radio></div>
                <div class="itemblock"><radio value="3" :checked="researchCarrier==3">省级</radio></div>
                </radio-group>
            </div>
            <div class="labname">科技人员情况（人数）</div>
            <div class="radiobox">
                <radio-group @change="changetyped">
                <div class="itemblock"><radio value="1" :checked="sciencePerson==1">0~10</radio></div>
                <div class="itemblock"><radio value="2" :checked="sciencePerson==2">10~15</radio></div>
                <div class="itemblock"><radio value="3" :checked="sciencePerson==3">15~50</radio></div>
                <div class="itemblock"><radio value="4" :checked="sciencePerson==4">大于等于50</radio></div>
                </radio-group>
                
            </div>
            <div class="labname">上年度研发费用（万元）</div>
            <div class="radiobox">
                <radio-group @change="changetypec">
                <div class="itemblock"><radio value="1" :checked="lastYearResearchCost==1">小于100</radio></div>
                <div class="itemblock"><radio value="2" :checked="lastYearResearchCost==2">100~200</radio></div>
                <div class="itemblock"><radio value="3" :checked="lastYearResearchCost==3">200~1000</radio></div>
                <div class="itemblock"><radio value="4" :checked="lastYearResearchCost==4">大于等于1000</radio></div>
                </radio-group>
                
            </div>
            <div class="labname">发明专利已授权数量是否达到4项</div>
            <div class="radiobox">
                <radio-group @change="changetypedf">
                <div class="itemblock"><radio value="1" :checked="inventNum==1">是</radio></div>
                <div class="itemblock"><radio value="2" :checked="inventNum==2">否</radio></div>
                </radio-group>
            </div>
            <div class="labname">专有科研设备资产原值总额（万）</div>
            <div class="radiobox">
                <radio-group @change="changetypesc">
                <div class="itemblock"><radio value="1" :checked="scientificDevice==1">0~200</radio></div>
                <div class="itemblock"><radio value="2" :checked="scientificDevice==2">200~500</radio></div>
                <div class="itemblock"><radio value="3" :checked="scientificDevice==3">大于500</radio></div>
                </radio-group>
            </div>
            <div class="nextstep mt16" @click="ceping">立即评估项目</div>
        </div>
        <div v-if="nowtype==2" class="pdbox">
            <h3 class="typetitle">{{companyName}}</h3>
            <div class="labname" v-if="showtime">企业注册时间</div>
            <div class="datepicker" v-if="showtime">
                <picker mode="date" :value="date" start="1900-01-01" end="2020-12-31" @change="bindDateChange" >
                    <view class="picker">
                    <span v-if="!date" class="tishi">请选择注册时间</span> {{date}}
                    </view>
                </picker>
            </div>
            <div class="labname">知识产权（可多选）</div>
            <div class="radiobox">
                <checkbox-group @change="changetypeef">
                    <!-- <div class="itemblock"><checkbox value="1" :disabled="isdisable==1" :checked="iptype==1">无</checkbox></div> -->
                    <div class="itemblock"><checkbox value="2"  :checked="iptype==2||iptype==4">在申请</checkbox></div>
                    <div class="itemblock"><checkbox value="3"  :checked="iptype==3||iptype==4">已授权</checkbox></div>
                </checkbox-group>
            </div>
            <div class="labname">上年度销售收入（万元）</div>
            <div class="radiobox">
                <radio-group @change="changetypef">
                <div class="itemblock"><radio value="1" :checked="lastYearSalesRevenues==1">0~100</radio></div>
                <div class="itemblock"><radio value="2" :checked="lastYearSalesRevenues==2">100~300</radio></div>
                <div class="itemblock"><radio value="3" :checked="lastYearSalesRevenues==3">300~5000</radio></div>
                <div class="itemblock"><radio value="4" :checked="lastYearSalesRevenues==4">大于5000</radio></div>
                </radio-group>
            </div>
            <div class="labname">社保缴纳人员情况（人数）</div>
            <div class="radiobox">
                <radio-group @change="changetypeg">
                <div class="itemblock"><radio value="1" :checked="socialSec==1">0~10</radio></div>
                <div class="itemblock"><radio value="2" :checked="socialSec==2">10人以上</radio></div>
                </radio-group>
            </div>
            <div class="labname">上年度研发费用（万元）</div>
            <div class="radiobox">
                <radio-group @change="changetypeh">
                <div class="itemblock"><radio value="1" :checked="lastYearResearchCosts==1">0~200</radio></div>
                <div class="itemblock"><radio value="2" :checked="lastYearResearchCosts==2">200以上</radio></div>
                </radio-group>
            </div>
            <div class="nextstep mt16" @click="ceping">立即评估项目</div>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            nowtype:1,
            companyName:'',
            isNewHigh: '',
            scientificDevice:'',
            lastYearSalesRevenue:'',
            researchCarrier:'',
            sciencePerson:'',
            lastYearResearchCost:'',
            inventNum:'',
            ip:'',
            date:'',
            dates:'',
            lastYearSalesRevenues:'',
            socialSec:'',
            lastYearResearchCosts:'',
            // outTech:'',
            // isdisable: 0,
            year: '',
            showtime: false,
            iptype:'',
            fromtype:'',
            savedata:{},
        }
    },
    onShow(){
        let rets = wx.getStorageSync('companydata')
        let cdatas = JSON.parse(rets)
        this.companyName=cdatas.companyName;
        this.isNewHigh= cdatas.isNewHigh-0;
        this.nowtype = this.isNewHigh;
        this.date = this.toymd(cdatas.registerTime);
        if(!this.date){
            this.showtime = true;
        }else{
            this.showtime = false;
        }
        let ret = wx.getStorageSync('savelocaldata')
        console.log(ret)
        if(ret){
            this.savedata =JSON.parse(ret);
            this.date = this.toymd(this.savedata.registerTime)
            this.showtime = false;
            if(this.savedata.isNewHigh ==2){
                this.ip=this.savedata.ip-0;
                this.lastYearSalesRevenues=this.savedata.lastYearSalesRevenue-0;
                this.socialSec= this.savedata.socialSec-0;
                this.lastYearResearchCosts=this.savedata.lastYearResearchCost-0;
                // this.outTech=this.savedata.outTech-0;
                
                // if(this.savedata.ip==1){
                //     this.isdisable = 2;
                // }else{
                //     this.isdisable =1;
                // }
                this.iptype = this.savedata.ip-0;
            }
            if(this.savedata.isNewHigh ==1){
                
                this.lastYearSalesRevenue=this.savedata.lastYearSalesRevenue-0;
                this.researchCarrier=this.savedata.researchCarrier-0;
                this.sciencePerson= this.savedata.sciencePerson-0;
                this.lastYearResearchCost=this.savedata.lastYearResearchCost-0;
                this.inventNum=this.savedata.inventNum-0;
                this.scientificDevice = this.savedata.scientificDevice-0;
            }
        }
        
        
        // let nowtime = new Date();
        // this.date = this.toymd(nowtime)
    },
    methods:{
        setreset(){
            // this.isdisable = 0;
            this.isNewHigh= '';
            this.lastYearSalesRevenue='';
            this.researchCarrier='';
            this.sciencePerson='';
            this.lastYearResearchCost='';
            this.inventNum='';
            this.ip='';
            this.date='';
            this.lastYearSalesRevenues='';
            this.socialSec='';
            this.lastYearResearchCosts='';
            // this.outTech='';
            this.scientificDevice = '';
            this.year='';
            this.iptype = '';
            this.showtime = false
        },
        // async gettime(){
        //     let data = {
        //         companyName: this.companyName,
        //         isNewHigh: this.isNewHigh
        //     }
        //     let res = await this.API.home.gettime(data);
        //     if(res.registerYear===null||res.registerYear===''){
        //         this.showtime = true
        //     }
        //     this.year = res.registerYear
        //     if(this.isNewHigh==2){
        //         this.nowtype = 3
                
        //     }
        //     if(this.isNewHigh==1){
        //         this.nowtype = 2;
                
        //     }
        //     console.log(res)
        // },
        tostamp(t){
            if(t){
                return new Date(t).getTime()
            }else{
                return ''
            }
            
        },
        toymd(t){
            if(t){
                let nowtime = new Date(t);
                let y = nowtime.getFullYear();
                let m = nowtime.getMonth() +1;
                let d = nowtime.getDate()
                let sm = m>9?m:'0'+m;
                let sd = d>9?d:'0'+d
                return  y+'-'+sm+'-'+sd
            }
            return ''
        },
        async postceping(data){
            try {
                let res = await this.API.home.postceping(data)
                let savedatas = JSON.stringify(data)
                wx.setStorageSync('savelocaldata',savedatas)
                // console.log(res,savedatas)
                let rests = JSON.stringify(res.list)
                wx.setStorageSync('cepingresult', rests);
                setTimeout(()=>{
                    this.$router.push({path:'/pages/index/result'})
                    this.setreset()
                },0)
                
            } catch (error) {
                
            }

        },
        bindDateChange(e){
            this.date = e.target.value;
            console.log(e.target.value)
        },
        changetype(e){
            this.isNewHigh = e.target.value
            
        },
        changetypea(e){
            this.lastYearSalesRevenue = e.target.value
        },
        changetypeb(e){
            this.researchCarrier = e.target.value
        },
        changetypec(e){
            this.lastYearResearchCost = e.target.value
        },
        changetyped(e){
            this.sciencePerson = e.target.value
        },
        changetypedf(e){
            this.inventNum = e.target.value;
        },
        changetypesc(e){
            this.scientificDevice = e.target.value;
        },

        changetypef(e){
            this.lastYearSalesRevenues = e.target.value
        },
        changetypeg(e){
            this.socialSec = e.target.value
        },
        changetypeh(e){
            this.lastYearResearchCosts = e.target.value
        },
        // changetypei(e){
        //     this.outTech = e.target.value
        // },
        changetypeef(e){
            let res = e.target.value;
            // if(res.indexOf('2')!=-1 ||res.indexOf('3')!=-1 ){
            //     this.isdisable = 1;
                
            // }else if(res.indexOf('1')!=-1){
            //     this.isdisable = 2;
            // }else{
            //     this.isdisable = 0
                
            // }
            if(res.indexOf('1')!=-1){
                this.ip = 1
                this.iptype =1
            }
            if(res.indexOf('2')!=-1&&res.length==1){
                this.ip = 2
                this.iptype =2
            }
            if(res.indexOf('3')!=-1&&res.length==1){
                this.ip = 3
                this.iptype =3
            }
            if(res.indexOf('2')!=-1&&res.indexOf('3')!=-1){
                this.ip = 4
                this.iptype =4
            }
            if(!res.length){
                this.ip = ''
                this.iptype = 0
            }
            console.log(this.ip)
        },
        back(){
            this.nowtype =1
        },
        ceping(){
            let data = {}
            if(this.isNewHigh ==2){
                if(!this.ip){
                    wx.showToast({
                        title: '请选择知识产权情况',        // 显示文本
                        icon:'none',          // 图标类型
                        duration:  2000,        // 关闭时间
                    })
                    return 
                }
                if(!this.lastYearSalesRevenues){
                    wx.showToast({
                        title: '请选择上年度销售收入',
                        icon:'none',  
                        duration:  2000, 
                    })
                    return false
                }
                if(!this.socialSec){
                    wx.showToast({
                        title: '请选择社保缴纳人员情况',
                        icon:'none',  
                        duration:  2000, 
                    })
                    return false
                }
                if(!this.lastYearResearchCosts){
                    wx.showToast({
                        title: '请选择上年度研发费用',
                        icon:'none',  
                        duration:  2000, 
                    })
                    return false
                }
                // if(!this.outTech){
                //     wx.showToast({
                //         title: '请选择委外技术开发情况',
                //         icon:'none',  
                //         duration:  2000, 
                //     })
                //     return false
                // }
                data = {
                    companyName: this.companyName,
                    isNewHigh: this.isNewHigh-0,
                    ip:this.ip-0,
                    lastYearSalesRevenue:this.lastYearSalesRevenues-0,
                    socialSec: this.socialSec-0,
                    lastYearResearchCost:this.lastYearResearchCosts-0,
                    // outTech:this.outTech-0,
                }
                
                if(this.year!==null&&this.year!==''){
                    data.registerYear = this.year
                }
                if(this.date){
                    data.registerTime = this.tostamp(this.date)
                }
            }
            if(this.isNewHigh ==1){
                if(!this.lastYearSalesRevenue){
                    wx.showToast({
                        title: '请选择上年度销售收入',
                        icon:'none',  
                        duration:  2000, 
                    })
                    return false
                }
                if(!this.researchCarrier){
                    wx.showToast({
                        title: '请选择科研载体',
                        icon:'none',  
                        duration:  2000, 
                    })
                    return false
                }
                if(!this.sciencePerson){
                    wx.showToast({
                        title: '请选择科技人员情况',
                        icon:'none',  
                        duration:  2000, 
                    })
                    return false
                }
                if(!this.lastYearResearchCost){
                    wx.showToast({
                        title: '请选择上年度研发费用',
                        icon:'none',  
                        duration:  2000, 
                    })
                    return false
                }
                if(!this.inventNum){
                    wx.showToast({
                        title: '请选择发明专利授权数量情况',
                        icon:'none',  
                        duration:  2000, 
                    })
                    return false
                }
                if(!this.scientificDevice){
                    wx.showToast({
                        title: '请选择专有科研设备资产原值',
                        icon:'none',  
                        duration:  2000, 
                    })
                    return false
                }
                data = {
                    companyName: this.companyName,
                    isNewHigh: this.isNewHigh-0,
                    lastYearSalesRevenue:this.lastYearSalesRevenue-0,
                    researchCarrier:this.researchCarrier-0,
                    sciencePerson: this.sciencePerson-0,
                    lastYearResearchCost:this.lastYearResearchCost-0,
                    inventNum:this.inventNum-0,
                    scientificDevice: this.scientificDevice-0
                }
            }
            if(!this.date){
                wx.showToast({
                    title: '请选择企业注册时间',        // 显示文本
                    icon:'none',          // 图标类型
                    duration:  2000,        // 关闭时间
                })
                return 
            }
            data.registerTime = this.tostamp(this.date)
            // console.log(data)
            // this.$router.push({path:'/pages/index/result'})
            this.postceping(data)
            
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
        },
        toback(){
            this.$router.go(-1)
        }
    },
}
</script>

<style lang="scss">
.kejipingce{
    min-height: 100%;
    background-color: #fff;
    font-family:'PingFangSC-Medium','PingFang SC';
    padding-bottom: 100px;
    padding-top: 170px;
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
    .typetitle{
        height:50px;
        font-size:36px;
        font-weight:500;
        color:rgba(36,125,255,1);
        line-height:50px;
        font-weight: 500;
        margin-top: 42px;
        margin-bottom: 54px;
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
        margin-bottom: 28px;
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
