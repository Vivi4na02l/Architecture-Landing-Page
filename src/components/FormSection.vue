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

    <form>
      <input id="txtName" type="text" placeholder="Name" />

      <input id="txtEmail" type="email" placeholder="Email" />

      <textarea name="Message" id="" cols="30" rows="10" placeholder="Message"></textarea>

      <input class="btn-submit" type="submit" value="Get in touch" />
    </form>
  </section>
</template>

<script>
export default {};
</script>

<style scoped>
@import "@/assets/styles/FormSection.css";
</style>
