<template>
  <v-card elevation="5">
    <v-row>
      <v-col align="start" class="pa-10 text-h5" cols="auto">
        <b>Recently Viewed</b>
      </v-col>
      <v-col align-self="center" align="end" class="mr-5">
        <JsonCSV
          :data="gallery">
          <v-btn>Download CSV</v-btn>
      </JsonCSV>
      </v-col>
    </v-row>
    <v-data-table
      class="pa-5"
      :headers="headers"
      :items="gallery"
      :loading="isLoading"
    >
      <template v-slot:loading>
        <v-skeleton-loader
          v-for="n in 5"
          :key="n"
          type="list-item-avatar-two-line"
          class="my-2"
        ></v-skeleton-loader>
      </template>

      <template #[`item.opt`]="{ item }">
        <v-menu offset-y z-index="1">
          <template v-slot:activator="{ attrs, on }">
            <v-btn icon v-bind="attrs" v-on="on">
              <v-icon>mdi-dots-horizontal</v-icon>
            </v-btn>
          </template>
          <v-list dense>
            <v-list-item @click.stop="status(item, 'Activate')">
              <v-list-item-content>
                <v-list-item-title>Edit</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
            <v-list-item @click.stop="status(item, 'Deactivate')">
              <v-list-item-content>
                <v-list-item-title>Delete</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-menu>
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
import JsonCSV from 'vue-json-csv'
export default {
  components:{
    JsonCSV
  },
  created() {
    this.loadData();
  },
  data() {
    return {
      selectedItem:{},
      isLoading: false,
      pools: [],
      dialogAdd:false,
      isAdd:true,
      gallery:[],
      headers: [
        { text: "ID", value: "id" },
        { text: "Industry", value: "category" },
        { text: "Timestamp", value: "timestamp" },
        { text: "Number of User's Selected", value: "quantity" },
        ,
      ],
    };
  },
  methods: {
    editItem(val){
      this.selectedItem=val
      this.dialogAdd=true
    },
    addItem(){
      this.isAdd=true
      this.dialogAdd=true
    },
    async status(data, status) {
      this.isLoading = true;
      const res = await this.$axios
        .patch(
          `/announcement/${data.id}/`,
          {
            is_active: status == "Deactivate" ? false : true,
          },
          {
            headers: {
              Authorization: `Bearer ${localStorage.getItem("token")}`,
            },
          }
        )
        .then((res) => {
          this.loadData();
        });
    },
    loadData() {
      this.galleryGetall();
    },
    async galleryGetall() {
      this.isLoading = true;
      const res = await this.$axios
        .get(`/demand/`, {
          headers: {
           
          },
        })
        .then((res) => {
          console.log(res.data);
          this.gallery = res.data;
          this.isLoading = false;
        });
    },
  },
};
</script>

<style>
</style>