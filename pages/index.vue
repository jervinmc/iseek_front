<template>
  <div>
    <div>
      <route />
    </div>
    <div>
      <home-hero />
    </div>
    <div>
      <about-us />
    </div>
    <div>
      <contact-container />
    </div>
    <!-- <div>
      <footer-all />
    </div> -->
  </div>
</template>

<script>
import ContactContainer from "../components/contact/ContactContainer.vue";
import FooterAll from "../components/footer/FooterAll.vue";
import Route from "../components/general/route.vue";
import AboutUs from "../components/home/AboutUs.vue";
import HomeHero from "../components/home/HomeHero.vue";
export default {
  components: { HomeHero, AboutUs, FooterAll, Route, ContactContainer },
  methods: {
    locatorButtonPressed() {
      navigator.geolocation.getCurrentPosition(
        (position) => {
          console.log(position.coords.latitude);
          console.log(position.coords.longitude);
        },
        (error) => {
          console.log(error.message);
        }
      );
    },
  },
  name: "IndexPage",
};
</script>
