<template>
  <div class="main-container">
    <h1>Gerenciar Pedidos</h1>
    <App_Dashboard />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import App_Dashboard from "../components/App_Dashboard.vue";

export default defineComponent({
  name: "PedidosView",
  components: {
    App_Dashboard,
  },
});
</script>
