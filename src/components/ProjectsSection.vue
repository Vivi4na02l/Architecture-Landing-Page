<template>
  <section>
    <h2 id="projects" ref="tagTitle" :class="{ titleActive: isTitleVisible }">
      Premium homes made by Axis Haus
    </h2>

    <article ref="tagArticle">
      <div class="body" :class="{ leftSideAnimation: isArticleVisible }">
        <header>
          <h3 class="project-nbr">0{{ currentSlide + 1 }}</h3>
          <h3 class="project-name">{{ slideContent.title }}</h3>
        </header>

        <div class="extra-info extra-info-1">
          <span>
            <p>{{ slideContent.year }}</p>

            <span class="location">
              <img src="../assets/images/icon-pin.png" alt="location pin icon" />
              <p>{{ slideContent.location }}</p>
            </span>
          </span>

          <p>
            {{ slideContent.description }}
          </p>
        </div>

        <div class="extra-info extra-info-2">
          <p>Scope</p>

          <span>
            <span>Architecture</span>
            <span>Engineering</span>
            <span>Construction</span>
          </span>
        </div>
      </div>

      <aside :class="{ rightSideAnimation: isArticleVisible }">
        <img :src="slideContent.img" alt="picture of the Hillside Residence" />
      </aside>
    </article>

    <footer>
      <div :class="{ leftSideAnimation: isArticleVisible }">
        <button class="btn-discussion">Discuss the Project</button>

        <span>
          <p>{{ slideContent.coords1 }}</p>
          <p>{{ slideContent.coords2 }}</p>
        </span>
      </div>

      <div class="carousel-btns" :class="{ rightSideAnimation: isArticleVisible }">
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
      </div>
    </footer>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, computed } from "vue";
import carouselHouse1 from "../assets/images/carousel-house-1.jpeg";
import carouselHouse2 from "../assets/images/carousel-house-2.jpg";
import carouselHouse3 from "../assets/images/carousel-house-3.jpg";
import carouselHouse4 from "../assets/images/carousel-house-4.jpg";
import carouselHouse5 from "../assets/images/carousel-house-5.jpg";

const slides = [
  {
    title: "Hillside Residence",
    year: 2024,
    location: "Los Angeles, USA",
    img: carouselHouse1,
    description:
      "A contemporary private residence designed with a strong focus on clarity, proportion and integration between architecture and landscape.",
    coords1: "34.0522º N",
    coords2: "118.2437º W",
  },
  {
    title: "Ridge House",
    year: 2025,
    location: "Seoul, South Korea",
    img: carouselHouse2,
    description:
      "A private home organized around an internal courtyard, allowing natural light, privacy and outdoor pace to shape the layout.",
    coords1: "37.5665º N",
    coords2: "126.9780º W",
  },
  {
    title: "Nordic Edge",
    year: 2023,
    location: "Oslo, Norway",
    img: carouselHouse3,
    description:
      "A modern residence organized through layered volumes, open living spaces and warm lighting that defines the architecture at night.",
    coords1: "59.9139º N",
    coords2: "10.7522º W",
  },
  {
    title: "Luminous Terrace",
    year: 2024,
    location: "Vancouver, Canada",
    img: carouselHouse4,
    description:
      "A refined living modern residential project, expansive, glazing and integrated lighting systems.",
    coords1: "49.2827º N",
    coords2: "123.1207º W",
  },
  {
    title: "Coastal Horizon",
    year: 2025,
    location: "Dubai, UAE",
    img: carouselHouse5,
    description:
      "A modern luxury residence shaped by strong geometric forms and terraces, offering panoramic skyline views and open living spaces.",
    coords1: "25.2048º N",
    coords2: "55.2708º W",
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

// ANIMATIONS
const tagTitle = ref(null);
const tagArticle = ref(null);

const isTitleVisible = ref(false);
const isArticleVisible = ref(false);

let titleObserver;
let articleObserver;

onMounted(() => {
  titleObserver = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        isTitleVisible.value = true;

        titleObserver.unobserve(entry.target); // animation doesn't happen again
      }
    },
    {
      threshold: 1, //title needs to be this amount visible on the screen to be activate this code section
    },
  );

  articleObserver = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        isArticleVisible.value = true;

        articleObserver.unobserve(entry.target); // animation doesn't happen again
      }
    },
    {
      threshold: 0.8, //article needs to be this amount visible on the screen to be activate this code section
    },
  );

  if (tagTitle.value) {
    titleObserver.observe(tagTitle.value); //what identifies what is being watched entering the screen
  }

  if (tagArticle.value) {
    articleObserver.observe(tagArticle.value); //what identifies what is being watched entering the screen
  }
});

onBeforeUnmount(() => {
  if (titleObserver) {
    titleObserver.disconnect();
  }
});
</script>

<style scoped>
@import "@/assets/styles/ProjectsSection.css";
</style>
