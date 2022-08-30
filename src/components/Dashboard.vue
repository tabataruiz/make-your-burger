<template>
  <Message :msg="msg" v-show="msg"></Message>
  <div class="burger-table">
    <div>
      <div class="burger-table-head">
        <div class="order-id">#</div>
        <div>Cliente</div>
        <div>Pão</div>
        <div>Carne</div>
        <div>Opcionais</div>
        <div>Ações</div>
      </div>
    </div>

    <div class="brger-table-rows">
      <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
        <div class="order-number">{{ burger.id }}</div>
        <div>{{ burger.nome }}</div>
        <div>{{ burger.pao }}</div>
        <div>{{ burger.carne }}</div>
        <div>
          <ul>
            <li v-for="(opcional, index) in burger.opcionais" :key="index">
              {{ opcional }}
            </li>
          </ul>
        </div>
        <div>
          <select
            name="status"
            class="status"
            @change="updateBurger($event, burger.id)"
          >
            <option
              v-for="status in status_data"
              :key="status.id"
              :value="status.tipo"
              :selected="burger.status === status.tipo"
            >
              {{ status.tipo }}
            </option>
          </select>
          <button class="btn-delete" @click="deleteBurger(burger.id)">
            Remover
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Message from "./Message.vue";

export default {
  name: "Dashboard",
  components: {
    Message
  },
  data() {
    return {
      burgers: null,
      burger_id: null,
      status_data: [],
      msg: null
    };
  },
  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/burgers");

      const data = await req.json();

      this.burgers = data;
    },
    async getStatus() {
      const req = await fetch("http://localhost:3000/status");

      const data = await req.json();

      this.status_data = data;
    },
    async deleteBurger(id) {
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "DELETE"
      });

      const res = await req.json();

      this.msg = `Pedido Nº ${id} removido com sucesso.`;

      setTimeout(() => (this.msg = ""), 5000);

      this.getPedidos();
    },
    async updateBurger(event, id) {
      const option = event.target.value;

      const dataJson = JSON.stringify({ status: option });

      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: dataJson
      });

      const res = await req.json();

      console.log(res);
    }
  },
  mounted() {
    this.getPedidos();
    this.getStatus();
  }
};
</script>

<style scoped>
.burger-table {
  max-width: 1200px;
  margin: 0 auto;
}

.burger-table-head,
.burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
}

.burger-table-head {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}

.burger-table-head div,
.burger-table-row div {
  width: 19%;
}

.burger-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #ccc;
}

.burger-table-head .order-id,
.burger-table-row .order-number {
  width: 5%;
}

select {
  padding: 12px 6px;
  margin-right: 12px;
}

.btn-delete {
  background: #222;
  color: #fcba03;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  border-radius: 3px;
  transition: 0.5s;
  cursor: pointer;
  font-weight: bold;
}

.btn-delete:hover {
  background: #fcba03;
  color: #222;
  border: 2px solid #fcba03;
}
</style>
