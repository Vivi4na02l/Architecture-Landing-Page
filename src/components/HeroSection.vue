<template>
  <section ref="tagSection" id="hero">
    <div></div>
    <div class="main-grid">
      <span class="title-xl" :class="{ leftSideAnimation: isSectionVisible }">
        <h2 class="title">High-end</h2>
        <h2 class="title">residential design</h2>

        <span class="title-description">
          <h2 class="title">& build</h2>

          <span>
            <button class="btn-discussion">Discuss the Project</button>
            <p>
              Our work is defined with careful thinking, technical precision and attention to
              detail.
            </p>
          </span>
        </span>
      </span>

      <span class="title-normal" :class="{ leftSideAnimation: isSectionVisible }">
        <h2 class="title">High-end residential design & build</h2>

        <span class="title-description">
          <button class="btn-discussion">Discuss the Project</button>
          <p>
            Our work is defined with careful thinking, technical precision and attention to detail.
          </p>
        </span>
      </span>

      <div class="cards" :class="{ rightSideAnimation: isSectionVisible }">
        <div class="card card-1">
          <h3>10+</h3>
          <p>years of experience</p>
        </div>

        <div class="card card-2">
          <h3>75+</h3>
          <p>completed projects</p>
        </div>

        <article class="card card-3">
          <img :src="slideContent.img" alt="modern house" />

          <aside>
            <header>
              <!-- add logo -->
            </header>

            <span>
              <h3>{{ slideContent.title }}</h3>
              <p>
                {{ slideContent.description }}
              </p>
            </span>

            <footer>
              <span class="indicators">
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
                <div
                  class="indicator indicator-4"
                  :class="currentSlide == 3 ? 'indicator-active' : ''"
                  @click="slidePage(3)"
                ></div>
                <div
                  class="indicator indicator-5"
                  :class="currentSlide == 4 ? 'indicator-active' : ''"
                  @click="slidePage(4)"
                ></div>
              </span>

              <span class="arrows">
                <div class="arrow arrow-left" @click="slidePage(-1)">🠜</div>
                <div class="arrow arrow-right" @click="slidePage(5)">🠞</div>
              </span>
            </footer>
          </aside>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, computed } from "vue";
import carouselHouse1 from "../assets/images/carousel-house-1.jpg";
import carouselHouse2 from "../assets/images/carousel-house-2.jpg";
import carouselHouse3 from "../assets/images/carousel-house-3.jpg";
import carouselHouse4 from "../assets/images/carousel-house-4.jpg";
import carouselHouse5 from "../assets/images/carousel-house-5.jpg";

const slides = [
  {
    title: "Hillside Residence",
    img: carouselHouse1,
    description:
      "A contemporary private residence designed with a strong focus on clarity, proportion and integration between architecture and landscape.",
  },
  {
    title: "Ridge House",
    img: carouselHouse2,
    description:
      "A private home organized around an internal courtyard, allowing natural light, privacy and outdoor pace to shape the layout.",
  },
  {
    title: "Nordic Edge",
    location: "Oslo, Norway",
    img: carouselHouse3,
    description:
      "A modern residence organized through layered volumes, open living spaces and warm lighting that defines the architecture at night.",
  },
  {
    title: "Luminous Terrace",
    location: "Vancouver, Canada",
    img: carouselHouse4,
    description:
      "A refined living modern residential project, expansive, glazing and integrated lighting systems.",
  },
  {
    title: "Coastal Horizon",
    location: "Dubai, UAE",
    img: carouselHouse5,
    description:
      "A modern luxury residence shaped by strong geometric forms and terraces, offering panoramic skyline views and open living spaces.",
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

//ANIMATIONS
const tagSection = ref(null);

const isSectionVisible = ref(false);

let observer;

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        if (entry.target == tagSection.value) {
          isSectionVisible.value = true;
        }

        observer.unobserve(entry.target); // animation doesn't happen again
      }
    },
    {
      threshold: 0.75, //section needs to be this amount visible on the screen to be activate this code section
    },
  );

  if (tagSection.value) {
    observer.observe(tagSection.value); //what identifies what is being watched entering the screen
  }
});

onBeforeUnmount(() => {
  if (observer) {
    observer.disconnect();
  }
});
</script>

<style scoped>
@import "@/assets/styles/HeroSection.css";
</style>
