<template>
  <div>
    <div>
        <route />
    </div>
    <div>
         <find-hero />
    </div>
    <div>
        <job-container/>
    </div>
  </div>
</template>

<script>
import FindHero from '../../components/findjob/FindHero.vue'
import JobContainer from '../../components/findjob/JobContainer.vue'
import Route from '../../components/general/route.vue'
export default {
  components: { FindHero, Route, JobContainer },

}
</script>

<style>

</style>