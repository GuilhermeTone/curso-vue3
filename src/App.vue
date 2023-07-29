<template>
  <App_Navbar :logo="logo_src" :alt="app_name" />
  <router-view />
  <App_Footer />
</template>

<script lang="ts">
import App_Navbar from "./components/App_Navbar.vue";
import App_Footer from "./components/App_Footer.vue";
import { defineComponent } from "vue";

export default defineComponent({
  components: {
    App_Navbar,
    App_Footer,
  },
  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Make Your Burguer",
    };
  },
});
</script>
<style>
* {
  font-family: Helvetica;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.main-container {
  margin: 50px;
  min-height: 250px;
}
h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}
</style>
