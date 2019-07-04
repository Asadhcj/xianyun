<template>
    <div class="container">
        <el-row type="flex" justify="space-between">
            <!-- 订单表单 -->
            <div class="main">
                 <ORDERFORM :data="insurances" @getseatInfo="handlepushseatInfo"/>
            </div>

            <!-- 侧边栏 -->
            <div class="aside">
                   <ORDERASIDE :data="data"/>       
            </div>
        </el-row>
    </div>
</template>

<script>
 import ORDERFORM from "@/components/air/orderForm";
 import ORDERASIDE from "@/components/air/orderAside"
export default {
    data(){
        return {
            insurances:[],
            data:{
                
            }
        }
    },
    components:{
         ORDERFORM,
         ORDERASIDE,
    },
    methods:{
        handlepushseatInfo(val){
            
        }
    },
    mounted(){
        this.$axios({
            url:"/airs/"+this.$route.query.id,
            method:"GET",
            params:this.$route.query.seat_xid
        }).then(res=>{
            const {insurances}=res.data
            this.insurances=insurances
        })
    }
}
</script>

<style lang="less" scoped>
    .container{
        width:1000px;
        margin:20px auto;
    }
    
    /*aside*/
    .aside{
        width: 350px;
        height: fit-content;
        border:1px #ddd solid;
    }
</style>