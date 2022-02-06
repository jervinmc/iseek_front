<template>
  <div style="height:100px" class="d-flex align-center justify-center">
    <v-row class="pr-10 px-10" align="center">
        <v-col>
            <v-img src="/logo.png" height="100" width="100" contain></v-img>
        </v-col>
        <v-spacer />
        <v-col cols="auto" @click="route('')" style="cursor:pointer">
            <div>
               <b> Home</b>
            </div>
        </v-col>
        <v-col cols="auto">
            <div>
               <b> About</b>
            </div>
        </v-col>
        <!-- <v-col cols="auto">
            <div>
               <b>Employers</b>
            </div>
        </v-col>
        <v-col cols="auto">
            <div>
               <b> Services</b>
            </div>
        </v-col> -->
        <v-col cols="auto">
            <div>
               <b> Contact</b>
            </div>
        </v-col>
        <!-- <v-col cols="auto">
            <div>
               <b>Applicants</b>
            </div>
        </v-col> -->
        <v-col cols="auto" @click="route('jobs')">
            <v-btn outlined depressed color="#6609af" dark> Find Jobs </v-btn>
        </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
    methods:{
        route(link){
            window.location.href="/"+link
        },
    }
}
</script>

<style>

</style>