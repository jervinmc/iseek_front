<template>
  <div class="px-10">
      <div class="text-h4">
          <b>Dashboard</b>
      </div>
     <v-row class="pt-5">
         <v-col align="center" @click="route('usermanagement')" >
            <v-card height="250" width="250" elevation="5" align="center" style="cursor:pointer">
                <v-icon size="120">mdi-account-multiple</v-icon>
                <div class="text-h5">
                   <b> Users</b>
                </div>
                <div class="text-h3 green--text pt-5">
                    <b>{{users.length}}</b>
                </div>
            </v-card>
         </v-col>
         <v-col align="center" @click="route('logs')" >
               <v-card height="250" width="250" elevation="5" align="center" style="cursor:pointer">
                <v-icon size="120">mdi-text-box-search-outline</v-icon>
                <div class="text-h5">
                   <b>Job Search</b>
                </div>
                <div class="text-h3 green--text pt-5">
                    <b>{{search_list.length}}</b>
                </div>
            </v-card>
         </v-col>
         <v-col align="center" @click="route('demand')" >
               <v-card height="250" width="250" elevation="5" align="center" style="cursor:pointer">
                <v-icon size="120">mdi-text-box-search-outline</v-icon>
                <div class="text-h5">
                   <b>Visit Website</b>
                </div>
                <div class="text-h3 green--text pt-5">
                    <b>{{demand_list.length}}</b>
                </div>
            </v-card>
         </v-col>
     </v-row>
     <div class="py-10" align="center">
    <v-card class="pa-10" elevation="5">
        <v-row>
            <v-col>
                <div class="text-h5" align="start">
                    <b>Top 3 Most Search:</b>
                </div>
                <div class="pie_chart"  style="height:280px" align="center" v-if="this.chartData1.datasets[0].data.length!=0">
                    <pie-chart :data="chartData1" :options="chartOptions"></pie-chart>
                </div>
            </v-col>
            <v-col>
                <div class="text-h5" align="start">
                    <b>Top 3 Most Viewed:</b>
                </div>
                <div class="pie_chart"  style="height:280px" align="center" v-if="this.chartData.datasets[0].data.length!=0">
                    <pie-chart :data="chartData" :options="chartOptions"></pie-chart>
                </div>
            </v-col>
        </v-row>
     </v-card>
     </div>
     <!-- <div class="pt-10">
         <v-card  elevation="5">
             <div style="">
                  <v-sparkline
                  height="50"
                    :labels="labels"
                    :value="value"
                    color="green"
                    line-width="1"
                    padding="16"
                    ></v-sparkline>
             </div>
         </v-card>
     </div> -->
       <div class="py-10">
            <v-card elevation="5"  width="100vw"> 
                <v-row class="pa-5">
                    <v-col>
                        <div class="text-h5">
                            <b>Top Search List:</b>
                        </div>
                        <div class="text-h6 pa-5" v-if="search_list.length>0">
                           <b>  1. {{search_list[0].search_location}} - {{search_list[0].search_job}}</b>
                        </div>
                        <div>
                            <v-divider></v-divider>
                        </div>
                        <div class="text-h6 pa-5" v-if="search_list.length>1">
                              2. {{search_list[1].search_location}} - {{search_list[1].search_job}}
                        </div>
                        <div>
                            <v-divider></v-divider>
                        </div>
                        <div class="text-h6 pa-5" v-if="search_list.length>2">
                            3.  {{search_list[2].search_location}} - {{search_list[2].search_job}}
                        </div>
                    </v-col>
                     <v-col>
                        <div class="text-h5">
                            <b>Top Viewed:</b>
                        </div>
                        <div class="text-h6 pa-5" v-if="demand_list.length>0">
                           <b>  1. {{demand_list[0].category}}</b>
                        </div>
                        <div>
                            <v-divider></v-divider>
                        </div>
                        <div class="text-h6 pa-5" v-if="demand_list.length>1">
                              2. {{demand_list[1].category}}
                        </div>
                        <div>
                            <v-divider></v-divider>
                        </div>
                        <div class="text-h6 pa-5" v-if="demand_list.length>2">
                            3.  {{demand_list[2].category}}
                        </div>
                    </v-col>
                </v-row>
            </v-card>
       </div>
  </div>
</template>

<script>
import PieChart from "./PieChart.js";
export default {
    components:{
        PieChart,
    },
    created(){
        this.loadData()
    },
    data(){
        return{
        chartData1: {
        responsive:false,
        hoverBackgroundColor: "red",
        hoverBorderWidth: 10,
        labels: [],
        datasets: [
          {
            label: "Data One",
            backgroundColor: ['#E3C790', '#344557'],
            data: []
          }
        ]
      },
      chartData: {
        responsive:false,
        hoverBackgroundColor: "red",
        hoverBorderWidth: 10,
        labels: [],
        datasets: [
          {
            label: "Data One",
            backgroundColor: ['#E3C790', '#344557'],
            data: []
          }
        ]
      },
      chartOptions: {
        chart: {
          title: 'Company Performance',
          subtitle: 'Sales, Expenses, and Profit: 2014-2017',
        },
      },
            users:[],
            search_list:[],
            demand_list:[]
        }
    },
    methods:{
        route(val){
            this.$router.push('/admin/'+val)
        },
        loadData(){
                this.searchGetall()
                this.usersGetall()
                this.demandGetall()
        },
       async usersGetall(){
            const res = await this.$axios
                .get(`/users/`, {
                headers: {
                    Authorization: `Bearer ${localStorage.getItem("token")}`,
                },
                })
                .then((res) => {
                console.log(res.data);
                this.users = res.data;
                
                });
        },
      
      async demandGetall(){
           this.isLoading = true;
            const res = await this.$axios
                .get(`/demand/`, {
                    headers: {
                        
                    },
                })
                .then((res) => {
                this.demand_list = res.data;
                this.demand_list.map(item=>{
              if(this.chartData.datasets[0].data.length>=3){
              }
              else {
                  this.chartData.labels.push(item.category)
                  this.chartData.datasets[0].data[this.chartData.datasets[0].data.length]=item.quantity
              }   
          })
        });
      },
      async searchGetall(){
      const res = await this.$axios
        .get(`/mostsearch/`, {
          headers: {
           
          },
        })
        .then((res) => {
          console.log(res.data);
          this.search_list = res.data;
          this.search_list.map(item=>{
              if(this.chartData1.datasets[0].data.length>=3){
              }
              else {
                  this.chartData1.labels.push(item.search_location + '-' + item.search_job)
                  this.chartData1.datasets[0].data[this.chartData1.datasets[0].data.length]=item.quantity
              }   
          })
        });
      }
    }

}
</script>

<style>
.pie_chart {
   margin: 0px 0px 30px 20px;
    max-width: 250px;
  }

</style>