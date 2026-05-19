<template>
  <section>
    <h2 ref="tagTitle" :class="{ titleActive: isTitleVisible }">Premium homes made by Axis Haus</h2>

    <article>
      <div class="body">
        <header>
          <h3 class="project-nbr">01</h3>
          <h3 class="project-name">Hillside Residence</h3>
        </header>

        <div class="extra-info extra-info-1">
          <span>
            <p>2024</p>

            <span class="location">
              <img src="../assets/images/icon-pin.png" alt="location pin icon" />
              <p>Los Angeles, USA</p>
            </span>
          </span>

          <p>
            A contemporary private residence designed with a strong focus on clarity, proportion and
            integration between architecture and landscape.
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

      <aside>
        <img src="../assets/images/carousel-house-1.jpeg" alt="picture of the Hillside Residence" />
      </aside>
    </article>

    <footer>
      <div>
        <button class="btn-discussion">Discuss the Project</button>

        <span>
          <p>34.0522º N</p>
          <p>118.2437º W</p>
        </span>
      </div>

      <div class="carousel-btns">
        <span class="indicators">
          <div class="indicator indicator-active indicator-1"></div>
          <div class="indicator indicator-2"></div>
          <div class="indicator indicator-3"></div>
          <div class="indicator indicator-4"></div>
          <div class="indicator indicator-5"></div>
        </span>

        <span class="arrows">
          <div class="arrow arrow-left">🠜</div>
          <div class="arrow arrow-right">🠞</div>
        </span>
      </div>
    </footer>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const tagTitle = ref(null);
const isTitleVisible = ref(false);

let observer;

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        isTitleVisible.value = true;

        observer.unobserve(entry.target); // animation doesn't happen again
      }
    },
    {
      threshold: 1, //title needs to be this amount of time on the screen to be activate this code section
    },
  );
  if (tagTitle.value) {
    observer.observe(tagTitle.value); //what identifies what is being watched entering the screen
  }
});

onBeforeUnmount(() => {
  if (observer) {
    observer.disconnect();
  }
});
</script>

<style scoped>
@import "@/assets/styles/ProjectsSection.css";
</style>
