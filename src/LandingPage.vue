<template>
  <div>
    <div class="bg-image">
      <HeroSection />
      <AboutSection />
    </div>
  </div>
</template>

<script>
import HeroSection from "./components/HeroSection.vue";
import AboutSection from "./components/AboutSection.vue";

export default {
  components: {
    HeroSection,
    AboutSection,
  },
};
</script>

<style scoped>
.bg-image {
  width: 100%;
  height: 120vh;

  background-image:
    linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.2)),
    url("./src/assets/images/house-background.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 50%;
}
</style>
