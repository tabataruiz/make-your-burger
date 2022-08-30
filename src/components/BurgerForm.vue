<template>
  <div class="burger-form">
    <p>Componente de mensagem</p>

    <div>
      <form class="burger-g" @submit="createBurger">
        <div class="input-container">
          <label for="nome">Nome do Cliente</label>
          <input
            type="text"
            id="nome"
            name="nome"
            v-model="nome"
            placeholder="Digite o seu nome"
          />
        </div>

        <div class="input-container">
          <label for="pao">Escolha o pão</label>
          <select name="pao" id="pao" v-model="pao">
            <option value="">Selecione o seu pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
              {{ pao.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label for="pao">Escolha a carne</label>
          <select name="carne" id="carne" v-model="carne">
            <option value="">Selecione a carne</option>
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
              {{ carne.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container opcionais">
          <label for="opcionais">Selecione os opcionais</label>
          <div
            class="checkbox-container"
            v-for="opcional in opcionaisdata"
            :key="opcional.id"
          >
            <input
              type="checkbox"
              name="opcionais"
              v-model="opcionais"
              :value="opcional.tipo"
            />
            <span>{{ opcional.tipo }}</span>
          </div>
        </div>

        <div class="input-container">
          <button type="submit">Criar meu Burger!</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "BurgerForm",
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisdata: null,
      nome: null,
      pao: null,
      carne: null,
      opcionais: [],
      mensagem: null
    };
  },
  methods: {
    async getIngredients() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisdata = data.opcionais;
    },
    async createBurger(e) {
      e.preventDefault();

      const data = {
        nome: this.nome,
        carne: this.carne,
        pao: this.pao,
        opcionais: Array.from(this.opcionais),
        status: "Solicitado"
      };

      const dataJson = JSON.stringify(data);

      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson
      });

      const res = await req.json();

      this.nome = "";
      this.carne = "";
      this.pao = "";
      this.opcionais = "";
    }
  },
  mounted() {
    this.getIngredients();
  }
};
</script>

<style scoped>
.burger-form {
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin: 20px;
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

.input-container.opcionais {
  flex-direction: row;
  flex-wrap: wrap;
}

.input-container.opcionais label {
  width: 100%;
}

.checkbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}

.checkbox-container input {
  margin-top: 2px;
  width: auto;
}

.checkbox-container span {
  width: auto;
  margin-left: 6px;
  font-weight: bold;
}

button {
  background: #222;
  color: #fcba03;
  border: 2px solid #222;
  padding: 10px 50px;
  font-size: 16px;
  margin: 0 auto;
  border-radius: 3px;
  transition: 0.5s;
  cursor: pointer;
  font-weight: bold;
}

button:hover {
  background: #fcba03;
  color: #222;
  border: 2px solid #fcba03;
}
</style>
