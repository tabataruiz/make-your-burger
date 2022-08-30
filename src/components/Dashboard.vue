<template>
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
      <div class="burger-table-row">
        <div class="order-number">1</div>
        <div>Tabata</div>
        <div>Francês</div>
        <div>Picanha</div>
        <div>
          <ul>
            <li>Bacon</li>
            <li>Cebola</li>
          </ul>
        </div>
        <div>
          <select name="status" class="status">
            <option value="">Selecione</option>
          </select>
          <button class="btn-delete">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Dashboard"
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
