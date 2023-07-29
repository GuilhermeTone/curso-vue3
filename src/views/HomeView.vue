<template>
  <App_Banner />
  <div class="main-container">
    <h1>Monte o seu burguer</h1>
    <Burger_Form />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import App_Banner from "../components/App_Banner.vue";
import Burger_Form from "../components/Burger_Form.vue";
export default defineComponent({
  name: "HomeView",
  components: {
    App_Banner,
    Burger_Form,
  },
});
</script>
