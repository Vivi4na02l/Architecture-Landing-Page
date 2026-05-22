<template>
  <section>
    <div class="indicators-nbr">
      <p
        class="indicator-nbr indicator-nbr-1"
        :class="currentSlide == 0 ? 'indicator-nbr-active' : ''"
        @click="slidePage(0)"
      >
        01
      </p>
      <p
        class="indicator-nbr indicator-nbr-2"
        :class="currentSlide == 1 ? 'indicator-nbr-active' : ''"
        @click="slidePage(1)"
      >
        02
      </p>
      <p
        class="indicator-nbr indicator-nbr-3"
        :class="currentSlide == 2 ? 'indicator-nbr-active' : ''"
        @click="slidePage(2)"
      >
        03
      </p>
    </div>

    <div class="body" :style="backgroundContent">
      <div>
        <h3>{{ slideContent.title }}</h3>
        <p>
          {{ slideContent.description }}
        </p>
      </div>
    </div>

    <div class="indicators">
      <div
        class="indicator indicator-1"
        :class="currentSlide == 0 ? 'indicator-active' : ''"
        @click="slidePage(0)"
      ></div>
      <div
        class="indicator indicator-2"
        :class="currentSlide == 1 ? 'indicator-active' : ''"
        @click="slidePage(1)"
      ></div>
      <div
        class="indicator indicator-3"
        :class="currentSlide == 2 ? 'indicator-active' : ''"
        @click="slidePage(2)"
      ></div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, computed } from "vue";
import formHouse1 from "../assets/images/form-house-1.jpg";
import formHouse2 from "../assets/images/form-house-2.jpg";
import formHouse3 from "../assets/images/form-house-3.jpeg";

const slides = [
  {
    title: "Who we work with",
    img: formHouse1,
    description:
      "We work with private clients who value clarity, thoughtful decisions and  structured approach to creating their homes.",
  },
  {
    title: "Initial contact",
    img: formHouse2,
    description:
      "You get in touch with us to discuss your goals, preferences and overall expectations for the project.",
  },
  {
    title: "Project briefing",
    img: formHouse3,
    description:
      "We define the scope, budget range, timeline and key requirements to establish a clear project brief.",
  },
];

const currentSlide = ref(0);

function slidePage(page) {
  if (page == 5 && currentSlide.value < 4) {
    currentSlide.value++;
  } else if (page == -1 && currentSlide.value > 0) {
    currentSlide.value--;
  } else if (page >= 0 && page <= 4) {
    currentSlide.value = page;
  }
}

const slideContent = computed(() => {
  return slides[currentSlide.value];
});

const backgroundContent = computed(() => {
  return {
    backgroundImage: `linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url(${slideContent.value.img})`,
  };
});
</script>

<style scoped>
@import "@/assets/styles/FormSection.css";
</style>
