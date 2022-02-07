<template>
  <div align="center" class="pa-10">
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
          <v-card class="pa-10" rounded="lg" width="1000" align="start" @click="routeLink(item.link)">
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
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchTitle:'',
        isLoading:true,
      job_list: [],
      searchValue:'',
      title:''
    };
  },
  created() {
    this.loadData();
  },
  methods: {
    routeLink(link){
      window.location.href=link
    },
    search(){
        this.jobs_list=[]
        this.isLoading=true
        this.$axios.get(`/search/${this.searchValue=='' ? 'all' : this.searchValue}/${this.searchTitle=='' ? 'all' : this.searchTitle}`,
        {headers:{
            
        }})
        .then((res)=>{
                this.isLoading=false
              // alert()
              this.job_list = res.data
        })
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

<style>
</style>