<template>
  <div align="center">
      <div class="text-h4 pt-10 pb-5" align="center">
         <b>Contact Us</b>
      </div>
      <div class="pb-5">
          We're so excited to hear from you
      </div>
      <v-row class="pb-10">
          <v-col cols="5" align="center">
              <v-card  width="500" elevation="5" class="pa-10">
                    <div>
                        <v-row>
                            <v-col align="start" cols="auto">
                                <v-icon size="50">mdi-map-marker</v-icon>
                            </v-col>
                            <v-col align="start">
                                <div class="text-h5">
                                   <b> Location</b>
                                </div>
                                <div>
                                    Eulogio 'Amang" Rorriguez Institute of Science and Technology
                                </div>
                            </v-col>
                        </v-row>
                    </div>
                    <div class="pt-10">
                        <v-row>
                            <v-col align="start" cols="auto">
                                <v-icon size="50">mdi-mail</v-icon>
                            </v-col>
                            <v-col align="start">
                                <div class="text-h5">
                                   <b> Email</b>
                                </div>
                                <div>
                                   iseekwebapp@gmail.com
                                </div>
                            </v-col>
                        </v-row>
                    </div>
                    <div class="pt-10">
                        <v-row>
                            <v-col align="start" cols="auto">
                                <v-icon size="50">mdi-phone</v-icon>
                            </v-col>
                            <v-col align="start">
                                <div class="text-h5">
                                   <b> Call</b>
                                </div>
                                <div>
                                   Smart: 09555555555 or Globe: 09955216823
                                </div>
                            </v-col>
                        </v-row>
                    </div>
              </v-card>
          </v-col>
          <v-col cols="7" align="center">
               <v-card  width="650" elevation="5" class="pa-5">
                   <v-row>
                       <v-col>
                           <div align="start">
                               Your Name
                           </div>
                           <v-text-field outlined v-model="contacts.name" ></v-text-field>
                       </v-col>
                        <v-col>
                           <div align="start">
                               Your Email
                           </div>
                           <v-text-field outlined v-model="contacts.email" ></v-text-field>
                       </v-col>
                   </v-row>
                   <v-row>
                       <v-col>
                           <div align="start">
                               Subject
                           </div>
                           <v-text-field outlined v-model="contacts.subject" ></v-text-field>
                       </v-col>
                   </v-row>
                   <v-row>
                        <v-col>
                           <div align="start">
                               Message
                           </div>
                           <v-textarea outlined v-model="contacts.message" ></v-textarea>
                       </v-col>
                   </v-row>
                   <v-col cols="auto" @click="sendEmail">
                        <v-btn outlined depressed color="#6609af" dark> Send Email </v-btn>
                    </v-col>
              </v-card>
          </v-col>
      </v-row>
  </div>
</template>

<script>
export default {
    methods:{
        sendEmail(){
            this.$axios.post('/inquire',{email:this.contacts.email,name:this.contacts.name,message:this.contacts.message},
            {
                headers:{

                }
            })
            .then(()=>{
                alert('sent!')
            })
        }
    },
    data(){
        return{
            contacts:[]
        }
    }
}
</script>

<style>

</style>