<template>
  <div class="pa-0">
    <v-img src="/banner_2.png" light>
      <v-sheet
        color="transparent"
        height="85vh"
        class="d-flex justify-center align-center"
      >
        <div align="center">
            <login-form />
        </div>
      </v-sheet>
    </v-img>
  </div>
</template>

<script>
import LoginForm from '../../components/admin/LoginForm.vue'
export default {
    components:{
        LoginForm
    }

}
</script>

<style>

</style>