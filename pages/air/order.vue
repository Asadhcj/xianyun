<template>
    <div class="container">
        <el-row type="flex" justify="space-between">
            <!-- 订单表单 -->
            <div class="main">
                 <ORDERFORM/>
            </div>

            <!-- 侧边栏 -->
            <div class="aside">
                   <!-- <ORDERASIDE/>        -->
            </div>
        </el-row>
    </div>
</template>

<script>
 import ORDERFORM from "@/components/air/orderForm.vue";
//  import ORDERASIDE from "@/components/air/orderAside.vue"
export default {
    components:{
         ORDERFORM,
        //  ORDERASIDE,
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