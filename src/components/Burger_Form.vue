<template>
  <div>
    <App_Message :msg="msg" v-show="msg" />
    <div>
      <form id="burger-form" @submit="createBurger">
        <div class="input-container">
          <label for="name">Nome do Cliente</label>
          <input
            type="text"
            name="name"
            id="name"
            v-model="name"
            placeholder="Digite o seu Nome"
          />
        </div>
        <div class="input-container">
          <label for="bread">Escolha o pão:</label>
          <select
            name="bread"
            id="bread"
            v-model="bread"
            placeholder="Digite o seu Nome"
          >
            <option value="">Selecione o Seu pão</option>
            <option v-for="bread in breads" :key="bread.id" :value="bread.tipo">
              {{ bread.tipo }}
            </option>
          </select>
        </div>
        <div class="input-container">
          <label for="meat">Escolha a Carne do seu Burguer:</label>
          <select
            name="meat"
            id="meat"
            v-model="meat"
            placeholder="Digite o seu Nome"
          >
            <option value="">Selecione o seu tipo de Carne</option>
            <option v-for="meat in meats" :key="meat.id" :value="meat.tipo">
              {{ meat.tipo }}
            </option>
          </select>
        </div>
        <div id="options-container" class="input-container">
          <label id="options-title" for="options">
            Selecione seus opcionais:
          </label>
          <div
            class="checkbox-container"
            v-for="opcional in optionsdata"
            :key="opcional.id"
          >
            <input
              type="checkbox"
              name="options"
              id="options"
              v-model="options"
              :value="opcional.tipo"
            />
            <span>{{ opcional.tipo }}</span>
          </div>
        </div>
        <div class="input-container">
          <input class="submit-btn" type="submit" value="Criar meu burger" />
        </div>
      </form>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";

import App_Message from "../components/App_Message.vue";

export default defineComponent({
  name: "Burger_Form",
  components: {
    App_Message,
  },
  data() {
    return {
      breads: null,
      meats: null,
      optionsdata: null,
      name: null,
      bread: null,
      meat: null,
      options: [],
      status: "",
      msg: "",
    };
  },
  methods: {
    async getIngredientes() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.breads = data.paes;
      this.meats = data.carnes;
      this.optionsdata = data.opcionais;
    },
    async createBurger(e: Event) {
      e.preventDefault();

      const data = {
        name: this.name,
        meat: this.meat,
        bread: this.bread,
        options: Array.from(this.options),
        status: "Solicitado",
      };

      const dataJson = JSON.stringify(data);

      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();

      this.msg = `Pedido N ${res.id} Realizado com Sucesso`;

      setTimeout(() => (this.msg = ""), 3000);
    },
  },
  mounted() {
    this.getIngredientes();
  },
});
</script>
<style scoped>
#burger-form {
  max-width: 400px;
  margin: 0 auto;
}
.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}
label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #fcba03;
}
input,
select {
  padding: 5px 10px;
  width: 300px;
}
#options-container {
  flex-direction: row;
  flex-wrap: wrap;
}
#options-title {
  width: 100%;
}
.checkbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}
.checkbox-container span,
.checkbox-container input {
  width: auto;
}
.checkbox-container span {
  margin-left: 6px;
  font-weight: bold;
}
.submit-btn {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}
.submit-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
