<template>
  <div>
    <NavBar />
    <div class="bg-image">
      <HeroSection />
      <AboutSection />
      <ProjectsSection />
      <ProcessSection />
      <FormSection />
      <FooterSection />
    </div>
  </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";
import HeroSection from "./components/HeroSection.vue";
import AboutSection from "./components/AboutSection.vue";
import ProjectsSection from "./components/ProjectsSection.vue";
import ProcessSection from "./components/ProcessSection.vue";
import FormSection from "./components/FormSection.vue";
import FooterSection from "./components/FooterSection.vue";

export default {
  components: {
    NavBar,
    HeroSection,
    AboutSection,
    ProjectsSection,
    ProcessSection,
    FormSection,
    FooterSection,
  },
};
</script>

<style scoped>
.bg-image {
  width: 100%;

  background-image:
    linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.2)),
    url("@/assets/images/house-background.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 50%;
}

@media screen and (max-height: 354px) {
  .bg-image {
    height: 220vh;
  }
}

@media screen and (min-height: 355px) and (max-height: 594px) {
  .bg-image {
    height: 170vh;
  }
}

@media screen and (min-height: 595px) {
  .bg-image {
    height: 120vh;
  }
}
</style>
