<template>
  <section class="ui two column centered grid">
    <div class="column">
      <form class="ui segment large form">
          <div class="field">
            <div class="ui right icon input large">
              <input
                type="text"
                placeholder="Enter your address"
                v-model="address"
                ref="autocomplete"
              />
              <i class="dot circle link icon" @click="locatorButtonPressed">test</i>
            </div>
        </div>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  methods:{
    locatorButtonPressed() {
  navigator.geolocation.getCurrentPosition(
     position => {
       console.log(position.coords.latitude);
       console.log(position.coords.longitude);
     },
     error => {
       console.log(error.message);
     },
  )   
}
  }
  ,
  name: 'IndexPage'
}
</script>
