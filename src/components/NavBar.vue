<template>
  <header>
    <nav :class="isOpen ? 'menuOpen' : ''">
      <h1>Axis Haus</h1>

      <div class="links">
        <a href="#hero">Home</a>
        <a href="#about">About</a>
        <a href="#projects">Projects</a>
        <a href="#process">Process</a>
      </div>

      <button>Get in touch</button>

      <span class="btnNavXS" @click="xsNavbar()">{{ isOpen ? "&#x2014;" : "X" }}</span>
    </nav>

    <Transition name="menu" @enter="onEnter" @leave="onLeave">
      <div v-if="isOpen" class="xsNavMenu">
        <ul class="xsMenuList">
          <li>
            <a href="#hero" @click="isOpen = false">Home</a>
          </li>
          <li>
            <a href="#about" @click="isOpen = false">About</a>
          </li>
          <li>
            <a href="#projects" @click="isOpen = false">Projects</a>
          </li>
          <li>
            <a href="#process" @click="isOpen = false">Process</a>
          </li>
        </ul>
      </div>
    </Transition>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const isOpen = ref(false);

function xsNavbar() {
  isOpen.value = !isOpen.value;
}

const preventScroll = (e) => {
  if (isOpen.value) {
    e.preventDefault();
  }
};

onMounted(() => {
  window.addEventListener("wheel", preventScroll, {
    passive: false,
  });

  window.addEventListener("touchmove", preventScroll, {
    passive: false,
  });
});

onUnmounted(() => {
  window.removeEventListener("wheel", preventScroll);

  window.removeEventListener("touchmove", preventScroll);
});
</script>

<style scoped>
@import "@/assets/styles/NavBar.css";
</style>
