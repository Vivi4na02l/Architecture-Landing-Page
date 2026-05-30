<template>
  <section>
    <div>
      <h3>Let's talk</h3>

      <span>
        <h4>Contact</h4>
        <span>
          <p>+1 222 333 444</p>
          <p>info@email.com</p>
        </span>
      </span>

      <span>
        <h4>Offices</h4>

        <span>
          <p>Los Angeles</p>
          <p class="address">9200 Sunset Blvd, Suite 800, Los Angeles, CA 90069</p>
        </span>

        <span>
          <p>New York</p>
          <p class="address">240 West 37th Street, Floor 10, New York, NY 10018</p>
        </span>
      </span>
    </div>

    <form @submit.prevent="handleSubmit">
      <input id="txtName" type="text" placeholder="Name" v-model="txtName" />

      <input id="txtEmail" type="email" placeholder="Email" v-model="txtEmail" />

      <textarea
        name="Message"
        id=""
        cols="30"
        rows="10"
        placeholder="Message"
        v-model="txtMessage"
      ></textarea>

      <input class="btn-submit" type="submit" value="Get in touch" />
    </form>

    <Transition name="menu" @enter="onEnter" @leave="onLeave">
      <span class="notificationWrapper" v-show="formSubmitted">
        <div class="notificationMessage">
          <p>Thank you {{ txtName }}!</p>
          <p>
            This contact form is part of a portfolio demonstration. Your message has not been sent
            and no data has been stored.
          </p>
        </div>
      </span>
    </Transition>
  </section>
</template>

<script setup>
import { ref } from "vue";

const formSubmitted = ref(false);
const txtName = ref("");
const txtEmail = ref("");
const txtMessage = ref("");

function handleSubmit() {
  formSubmitted.value = true;

  setTimeout(() => {
    formSubmitted.value = false;
  }, 5000);
}
</script>

<style scoped>
@import "@/assets/styles/FormSection.css";
</style>
