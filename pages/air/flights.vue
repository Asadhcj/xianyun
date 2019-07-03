<template>
    <div class="cantainter">
       <div class="main">
           <el-row type="flex" justify="space-between">
               <div class="flights-left">
                    <FLIGHTSFILTERS :data="datalist" @select="getflightslist"/>
                    <FLIGHTSHEADER/>
                    <div>
                        <FLIGHTSCONTENT
                        v-for="(item,index) in data.flights" 
                        :key="index"
                        :ticketInfo="item"/> 
                        <el-pagination
                        @size-change="handleSizeChange"
                        @current-change="handleCurrentChange"
                        :current-page="pageIndex"
                        :page-sizes="[5, 10, 15, 20]"
                        :page-size="pageSize"
                        layout="total, sizes, prev, pager, next, jumper"
                        :total="data.flights.total">
                        </el-pagination>
                    </div>
                  
               </div>
               <div class="flights-right"></div>
           </el-row>
       </div>
    </div>
</template>

<script>
    import FLIGHTSFILTERS from "@/components/air/flightsFilters";
    import FLIGHTSHEADER from "@/components/air/flightsheader";
    import  FLIGHTSCONTENT from "@/components/air/flightscontent"
export default {
    data(){
        return {
            data:{
                info:{},
                options:{},
                flights:[]
            },
            datalist:{
                info:{},
                options:{},
                flights:[] 
            },
            pageIndex:1,
            pageSize:5,
            newdata:{
                info:{},
                options:{},
                flights:[]
            }
        }
    },
    components:{
         FLIGHTSFILTERS,
         FLIGHTSHEADER,
         FLIGHTSCONTENT
    },
    methods:{
        handleSizeChange(val) {
        this.pageSize=val;
         this.getflightslist()
      },
      handleCurrentChange(val) {
        this.pageIndex=val;
         this.getflightslist()
      },
      getflightslist(arr){
          if(arr){
              this.pageIndex=1,
              this.newdata.flights=arr,
              this.pageSize=arr.length
          }
        this.data.flights=this.newdata.flights.slice(
            (this.pageIndex-1)*this.pageSize,
            this.pageSize*this.pageIndex)
      },
     
    },
    mounted(){
        this.$axios({
            url:"/airs",
            method:"GET",
            params:this.$route.query
        }).then(res=>{
            // console.log(res.data)
            this.datalist={...res.data}
            this.newdata={...res.data}
            this.data={...res.data};
            this.getflightslist()
        })
    }
   
}
</script>

<style scoped lang="less">
    .cantainter{
        width:100%;
        .main{
            width: 1000px;
            margin:0 auto;
        }
    }
</style>
