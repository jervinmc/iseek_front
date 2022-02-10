<template>
  <div align="center" class="pa-10">
     <v-container fluid class="pb-5">
          <v-row align="start" elevation="10">
            <v-col
              cols="3"
              :class="active_page == 0 ? 'tab active pa-5' : 'tab pa-5'"
              align="center"
              @click="active_page = 0"
            >
              <v-row class="tab-contents justify-start ml-6">
                <v-icon class="mr-2 action-icons"
                  >mdi-magnify</v-icon
                ><b
                  v-if="$vuetify.breakpoint.lg || $vuetify.breakpoint.xl"
                  class="tab-name"
                  >Search</b
                >
              </v-row>
            </v-col>
            <v-col
            cols="3"
              :class="active_page == 1 ? 'tab active pa-5' : 'tab pa-5'"
              align="center"
              @click="active_page = 1"
            >
              <v-row class="tab-contents justify-start ml-6">
                <v-icon class="mr-2 action-icons"
                  >mdi-file-find</v-icon
                ><b
                  v-if="$vuetify.breakpoint.lg || $vuetify.breakpoint.xl"
                  class="tab-name"
                  >Most Searched</b
                >
              </v-row>
            </v-col>
            <v-col
            cols="3"
              :class="active_page == 2 ? 'tab active pa-5' : 'tab pa-5'"
              align="center"
              @click="active_page = 2"
            > 
              <v-row class="tab-contents justify-start ml-6">
                <v-icon class="mr-2 action-icons"
                  >mdi-sine-wave</v-icon
                ><b
                  v-if="$vuetify.breakpoint.lg || $vuetify.breakpoint.xl"
                  class="tab-name"
                  >In Demand</b
                >
              </v-row>
            </v-col>
             <v-col
            cols="3"
              :class="active_page == 3 ? 'tab active pa-5' : 'tab pa-5'"
              align="center"
              @click="active_page = 3"
            > 
              <v-row class="tab-contents justify-start ml-6">
                <v-icon class="mr-2 action-icons"
                  >mdi-sine-wave</v-icon
                ><b
                  v-if="$vuetify.breakpoint.lg || $vuetify.breakpoint.xl"
                  class="tab-name"
                  >Highest Paying Jobs</b
                >
              </v-row>
            </v-col>

          </v-row>
        </v-container>
    <v-card elevation="5" v-if="active_page==0">
      <div align="center">
        <v-row>
            <v-spacer />
      <v-col cols="4">
        <v-text-field
          outlined
          v-model="searchValue"
          placeholder="Location"
          @keyup.enter="search"
          hide-details=""
        ></v-text-field>
      </v-col>
      <v-col cols="4">
        <v-text-field
          outlined
          v-model="searchTitle"
          @keyup.enter="search"
          hide-details=""
          placeholder="Job Title"
        ></v-text-field>
      </v-col>
      <v-col cols="auto" @click="route('jobs')" align-self="center">
        <v-btn outlined depressed color="#6609af" dark> Search </v-btn>
      </v-col>
    </v-row>
    </div>
    <div class="pt-10">
         <v-skeleton-loader
        v-if="isLoading"
        class="mx-auto"
        width="1200"
        type="card"
      ></v-skeleton-loader>
      <div v-for="item in job_list" :key="item" class="pb-5">
          <v-card class="pa-10" rounded="lg" width="1000" align="start" @click="routeLink(item.link,item.category)">
            <div>
              <v-row>
                <v-col>
                  <v-img
                    contain
                    :src="item.image"
                    height="100"
                    width="100"
                  ></v-img>
                </v-col>
                <v-col cols="10">
                  <div class="text-h6"><b>{{ item.jobTitle }}</b></div>
                  <!-- <div class="text-trunctate">
                    {{ sub_item.companyDescription }}
                  </div> -->
                  <div>
                    <v-icon>mdi-map-marker-outline</v-icon>
                    {{ item.location }}
                  </div>
                </v-col>
              </v-row>
              <div class="pt-10 text-truncate">
                {{ item.jobDescription }}<br />
              </div>
            </div>
          </v-card>
        </div>
      </div>
    </v-card>
        <v-card elevation="5" v-if="active_page==1">
    <div class="pt-10">
         <v-skeleton-loader
        v-if="isLoading"
        class="mx-auto"
        width="1200"
        type="card"
      ></v-skeleton-loader>
      <div v-for="item in mostsearch_list" :key="item" class="pb-5">
          <v-card class="pa-10" rounded="lg" width="1000" align="start" @click="routeLink(item.link,item.category)">
            <div>
              <v-row>
                <v-col>
                  <v-img
                    contain
                    :src="item.image"
                    height="100"
                    width="100"
                  ></v-img>
                </v-col>
                <v-col cols="10">
                  <div class="text-h6"><b>{{ item.jobTitle }}</b></div>
                  <!-- <div class="text-trunctate">
                    {{ sub_item.companyDescription }}
                  </div> -->
                  <div>
                    <v-icon>mdi-map-marker-outline</v-icon>
                    {{ item.location }}
                  </div>
                </v-col>
              </v-row>
              <div class="pt-10 text-truncate">
                {{ item.jobDescription }}<br />
              </div>
            </div>
          </v-card>
        </div>
      </div>
    </v-card>
        <v-card elevation="5" v-if="active_page==2">
      
    <div class="pt-10">
         <v-skeleton-loader
        v-if="isLoading"
        class="mx-auto"
        width="1200"
        type="card"
      ></v-skeleton-loader>
      <div v-for="item in mostdemand_list" :key="item" class="pb-5">
          <v-card class="pa-10" rounded="lg" width="1000" align="start" @click="routeLink(item.link,item.category)">
            <div>
              <v-row>
                <v-col>
                  <v-img
                    contain
                    :src="item.image"
                    height="100"
                    width="100"
                  ></v-img>
                </v-col>
                <v-col cols="10">
                  <div class="text-h6"><b>{{ item.jobTitle }}</b></div>
                  <!-- <div class="text-trunctate">
                    {{ sub_item.companyDescription }}
                  </div> -->
                  <div>
                    <v-icon>mdi-map-marker-outline</v-icon>
                    {{ item.location }}
                  </div>
                </v-col>
              </v-row>
              <div class="pt-10 text-truncate">
                {{ item.jobDescription }}<br />
              </div>
            </div>
          </v-card>
        </div>
      </div>
    </v-card>
     <v-card elevation="5" v-if="active_page==2">
      
    <div class="pt-10">
         <v-skeleton-loader
        v-if="isLoading"
        class="mx-auto"
        width="1200"
        type="card"
      ></v-skeleton-loader>
      <div v-for="item in rated_list" :key="item" class="pb-5">
          <v-card class="pa-10" rounded="lg" width="1000" align="start" @click="routeLink(item.link,item.category)">
            <div>
              <v-row>
                <v-col>
                  <v-img
                    contain
                    :src="item.image"
                    height="100"
                    width="100"
                  ></v-img>
                </v-col>
                <v-col cols="10">
                  <div class="text-h6"><b>{{ item.jobTitle }}</b></div>
                  <!-- <div class="text-trunctate">
                    {{ sub_item.companyDescription }}
                  </div> -->
                  <div>
                    <v-icon>mdi-map-marker-outline</v-icon>
                    {{ item.location }}
                  </div>
                </v-col>
              </v-row>
              <div class="pt-10 text-truncate">
                {{ item.jobDescription }}<br />
              </div>
            </div>
          </v-card>
        </div>
      </div>
    </v-card>
      <v-card elevation="5" v-if="active_page==3">
      
    <div class="pt-10">
         <v-skeleton-loader
        v-if="isLoading"
        class="mx-auto"
        width="1200"
        type="card"
      ></v-skeleton-loader>
      <div v-for="item in rated_list" :key="item" class="pb-5">
          <v-card class="pa-10" rounded="lg" width="1000" align="start" @click="routeLink(item.link,item.category)">
            <div>
              <v-row>
                <v-col>
                  <v-img
                    contain
                    :src="item.image"
                    height="100"
                    width="100"
                  ></v-img>
                </v-col>
                <v-col cols="10">
                  <div class="text-h6"><b>{{ item.jobTitle }}</b></div>
                  <!-- <div class="text-trunctate">
                    {{ sub_item.companyDescription }}
                  </div> -->
                  <div>
                    <v-icon>mdi-map-marker-outline</v-icon>
                    {{ item.location }}
                  </div>
                </v-col>
              </v-row>
              <div class="pt-10 text-truncate">
                {{ item.jobDescription }}<br />
              </div>
                   <div>
                SALARY : {{item.salary}}
              </div>
            </div>
          </v-card>
        </div>
      </div>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      active_page:0,
      searchTitle:'',
        isLoading:true,
      job_list: [],
      searchValue:'',
      title:'',
      mostdemand_list:[],
      mostsearch_list:[],
      rated_list:[]
    };
  },
  created() {
    this.loadData();
    this.mostsearch()
    this.mostsearch1()
    this.mostsearch2()
  },
  methods: {
    mostsearch(){
      this.$axios
            .get(
              `/mostdemanddata/`,
              {
                headers: {},
              }
            )
            .then((res) => {
                this.isLoading=false
              // alert()
              console.log(res.data)
              this.mostdemand_list = res.data;
            });
    },
      mostsearch1(){
      this.$axios
            .get(
              `/mostsearchdata/`,
              {
                headers: {},
              }
            )
            .then((res) => {
                this.isLoading=false
              // alert()
              console.log(res.data)
              this.mostsearch_list = res.data;
            });
    },
     mostsearch2(){
      this.$axios
            .get(
              `/highestpaidjob/`,
              {
                headers: {},
              }
            )
            .then((res) => {
                this.isLoading=false
              // alert()
              console.log(res.data)
              this.rated_list = res.data;
            });
    },
    routeLink(link,category){
      this.addToDemand(category)
      window.location.href=link
    },
    search(){
       try {
           this.jobs_list=[]
        this.isLoading=true
        this.$axios.get(`/search/${this.searchValue=='' ? 'all' : this.searchValue}/${this.searchTitle=='' ? 'all' : this.searchTitle}`,
        {headers:{
            
        }})
        .then((res)=>{
                this.isLoading=false
              // alert()
              this.job_list = res.data
              this.addToSearch()
        })
       } catch (error) {
          this.isLoading=false
       }
    },
  async  addToSearch(){
    this.$axios.post('/mostsearch/',{search_job:this.searchTitle,search_location:this.searchValue},{headers:{
      
    }})
    },
    async  addToDemand(category){
    this.$axios.post('/demand/',{category:category},{headers:{
      
    }})
    },
    loadData() {
      navigator.geolocation.getCurrentPosition(
        (position) => {
          this.$axios
            .get(
              `/getdata/${position.coords.latitude}/${position.coords.longitude}`,
              {
                headers: {},
              }
            )
            .then((res) => {
                this.isLoading=false
              // alert()
              console.log(res.data)
              this.job_list = res.data;
            });
          console.log(position.coords.latitude);
          console.log(position.coords.longitude);
        },
        (error) => {}
      );
    },
  },
};
</script>

<style lang="scss">
.tab {
  margin-right: -5px;
  background: #ececec;
  border-radius: 20px 60px 0px 0px;
  cursor: pointer;
  box-shadow: 0px 0px 2px #888888;
  &:hover {
    background: #fff;
  }
  &.active {
    background: #fff;
    // font-weight: bold;
    color: primary;
    // font-size: 20px;
    font-family: avenir-black;
    z-index: 1;
    box-shadow: 0px 0px 0px;
  }
}
</style>