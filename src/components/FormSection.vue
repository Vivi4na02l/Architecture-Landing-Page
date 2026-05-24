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

    <div class="body" :style="backgroundContent" ref="carouselSection">
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
import { ref, onMounted, onUnmounted, computed } from "vue";
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

// SCROLLING THROUGH PAGES
const carouselSection = ref(null);
const isAnimating = ref(false);
const isLocked = ref(false); //var used to regulate if scroll scrolls through page or thro the carousel slides

const handleScroll = (e) => {
  if (!isLocked.value) {
    return;
  }

  e.preventDefault(); //stops page from scrolling

  if (isAnimating.value) {
    // if animation is ongoing, doesn't activate it again
    return;
  }

  // isAnimating.value = true; // activates animation

  console.log(currentSlide.value, slides.length);

  if (e.deltaY > 0) {
    // checks if scroll is going down
    if (currentSlide.value == slides.length - 1) {
      // if it's on the last slide
      isLocked.value = false; // unlocks scroll so scroll scrolls the page again
    } else {
      slidePage(5); // goes to next slide
    }
  } else {
    // if it is going up
    if (currentSlide.value == 0) {
      isLocked.value = false;
    } else {
      slidePage(-1); // goes to slide before
    }
  }
};

onMounted(() => {
  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.intersectionRatio >= 0.95) {
        isLocked.value = true; // locks scroll when carousel enters viewport
      }
    },
    {
      threshold: 0.95,
    },
  );

  observer.observe(carouselSection.value);

  window.addEventListener("wheel", handleScroll, {
    passive: false,
  });

  onUnmounted(() => {
    observer.disconnect();

    window.removeEventListener("wheel", handleScroll);
  });
});

window.addEventListener("wheel", () => {
  console.log(currentSlide.value, slides.length, isLocked.value);
});
</script>

<style scoped>
@import "@/assets/styles/FormSection.css";
</style>
