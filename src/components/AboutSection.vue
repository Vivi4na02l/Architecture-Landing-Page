<template>
  <div class="bg-fade"></div>
  <section id="about">
    <div ref="tagTitle" class="about-title" :class="{ aboutActive: isTitleVisible }">
      <h2>A modern studio with a clear focus</h2>

      <span>
        <p>
          Aris House is a team working at the interaction of real estate, architecture, and
          technology.
        </p>
        <button class="btn-check">Check projects</button>
      </span>
    </div>

    <div class="grid-cards">
      <article
        ref="card1"
        class="cards card-1 card-black-bg"
        :class="{ cardActive: areCardsVisible }"
      >
        <header>
          <h3>01</h3>
          <div class="logo-white-bg">X</div>
        </header>

        <h4>Focused expertise</h4>
        <p>
          We concentrate on a limited number of projects to ensure full attention, consistency and
          control at every stage of the process
        </p>
      </article>

      <article
        class="cards card-2 card-white-bg"
        :class="{ 'cardActive card2Delay': areCardsVisible }"
      >
        <header>
          <h3>02</h3>
          <div class="logo-black-bg">X</div>
        </header>

        <h4>Thoughtful execution</h4>
        <p>
          Every element is carefully considered - from overall composition to the smallest
          architectural and technical decision, with precision.
        </p>
      </article>

      <article
        class="cards card-3 card-black-bg"
        :class="{ 'cardActive card3Delay': areCardsVisible }"
      >
        <header>
          <h3>03</h3>
          <div class="logo-white-bg">X</div>
        </header>

        <h4>Long-term quality</h4>
        <p>
          Our work is guided by durability, relevance and carefully developed solutions that remain
          strong, refined and appropriate over time.
        </p>
      </article>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

let titleObserver;
let cardObserver;

const tagTitle = ref(null);
const card1 = ref(null);

const isTitleVisible = ref(false);
const areCardsVisible = ref(false);

onMounted(() => {
  titleObserver = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        if (entry.target == tagTitle.value) {
          isTitleVisible.value = true;
        }

        titleObserver.unobserve(entry.target); // animation doesn't happen again
      }
    },
    {
      threshold: 1, //title needs to be this amount visible on the screen to be activate this code section
    },
  );

  cardObserver = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        if (entry.target == card1.value) {
          areCardsVisible.value = true;
        }

        cardObserver.unobserve(entry.target); // animation doesn't happen again
      }
    },
    {
      threshold: 0.75, //card1 needs to be this amount visible on the screen to be activate this code section
    },
  );

  if (tagTitle.value) {
    titleObserver.observe(tagTitle.value); //what identifies what is being watched entering the screen
  }

  if (card1.value) {
    cardObserver.observe(card1.value);
  }
});

onBeforeUnmount(() => {
  if (titleObserver) {
    titleObserver.disconnect();
  }

  if (cardObserver) {
    cardObserver.disconnect();
  }
});
</script>

<style scoped>
@import "@/assets/styles/AboutSection.css";
</style>
