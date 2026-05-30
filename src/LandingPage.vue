<template>
  <div>
    <div class="bg-image">
      <NavBar />
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
  height: 120vh;

  background-image:
    linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.2)),
    url("@/assets/images/house-background.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 50%;
}
</style>
