<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpences from "./IncomeExpences.vue";
import ListTransaction from "./components/ListTransaction.vue";
import addTransaction from "./components/addTransaction.vue";

import { ref, computed, onMounted } from "vue";
import { useToast } from "vue-toastification";

onMounted(() => {
  const transaccionesGuardadas = JSON.parse(
    localStorage.getItem("transactions")
  );
  if (transaccionesGuardadas) {
    transactions.value = transaccionesGuardadas;
  }
});

const toast = useToast();
const transactions = ref([
  {
    id: 1,
    text: "Flor",
    amount: -19.99,
  },
  {
    id: 2,
    text: "Salario",
    amount: 200.99,
  },
  {
    id: 3,
    text: "Libro",
    amount: -39.99,
  },
  {
    id: 4,
    text: "Camara",
    amount: 69.99,
  },
]);

const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

const outcome = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

const handleTransaccionEmitida = (datosTransaccion) => {
  // console.log(datosTransaccion)
  transactions.value.push({
    id: generarIdUnica(),
    text: datosTransaccion.text,
    amount: datosTransaccion.amount,
  });

  guardarTransacciones();

  toast.success("Se ha añadido correctamente.");
  return;
};

const generarIdUnica = () => {
  return Math.floor(Math.random() * 100000);
};

const handleTransaccionBorrada = (id) => {
  // console.log(id)
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );
  guardarTransacciones();
  toast.success("Transacción eliminada.");
};

const guardarTransacciones = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};
</script>

<template>
  <div>
    <Header />
    <div class="container">
      <Balance :total="+total" />
      <IncomeExpences :income="+income" :expenses="+outcome" />
      <ListTransaction
        :transactions="transactions"
        @transaccionBorrada="handleTransaccionBorrada"
      />
      <addTransaction @transaccionEmitida="handleTransaccionEmitida" />
    </div>
  </div>
</template>

<style scoped>
</style>
