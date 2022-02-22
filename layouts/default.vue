<template>
  <v-app dark>
    <v-app-bar :clipped-left="clipped" fixed app elevation="0" v-if="$route.name=='jobs' || $route.name=='index'">
      <v-icon> mdi-mail </v-icon>
      <v-col cols="auto"> iseekwebapp@gmail.com</v-col>
      <v-icon>
        mdi-phone
      </v-icon>
      <v-col>
        Smart : 09555555555 or Globe: 09955216823 
      </v-col>
      <v-spacer />
      <v-icon class="mr-5" @click="route('twitter')">
         mdi-twitter
      </v-icon>
        <v-icon class="mr-5" @click="route('facebook')">
          mdi-facebook
        </v-icon>
    </v-app-bar>
     <v-app-bar v-else :clipped-left="clipped" fixed app elevation="0" >
       <div align="start">
         <v-img src="/logo.png" height="50" width="100" contain></v-img>
       </div>
      <v-spacer />
      <v-icon class="mr-5" @click="routeAdmin('admin/dashboard')">
         mdi-home-analytics
      </v-icon>
      <v-icon class="mr-5" @click="routeAdmin('admin/logs')">
         mdi-magnify
      </v-icon>
      <v-icon class="mr-5" @click="routeAdmin('admin/demand')">
         mdi-poll
      </v-icon>
        <v-icon class="mr-5" @click="routeAdmin('admin/usermanagement')">
          mdi-account-multiple
        </v-icon>
    </v-app-bar>
    <v-main>
      <v-container fluid class="pa-0">
        <Nuxt  />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  created(){

  },
  methods:{
    route(link){
      if(link == 'facebook') {
        window.location.href="https://www.facebook.com/Iseek-110866381512433"
      }
      else{
         window.location.href="https://twitter.com/iseekwebapp"
      }
    },
    routeAdmin(link){
      window.location.href="/"+link
    }
  },
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: "mdi-apps",
          title: "Welcome",
          to: "/",
        },
        {
          icon: "mdi-chart-bubble",
          title: "Inspire",
          to: "/inspire",
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "Vuetify.js",
    };
  },
};
</script>
