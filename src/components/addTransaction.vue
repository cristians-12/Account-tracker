<template>
    <div>
        <h3>Añadir nueva transacción</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Nombre de transacción</label>
      <input type="text" id="text" v-model="text" placeholder="Ingrese el nombre de la transacción." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Cantidad <br />
        (Negativa - expense, Positiva - income)</label
      >
      <input
        type="text"
        id="amount"
        placeholder="Ingrese el valor..."
        v-model="amount"
      />
    </div>
    <button class="btn">Añadir transacción</button>
  </form>
    </div>
</template>

<script setup>
  import { ref, defineProps } from "vue";
  import { useToast } from "vue-toastification";

  const text = ref('');
  const amount = ref('');

  const toast = useToast();
  const emit = defineEmits(['transaccionEmitida']);

  const onSubmit = ()=>{
    if(!text.value || !amount.value){
      toast.error("Los dos campos deben estar llenos.");
      return;
    }

    const datosTransaccion = {
      text: text.value,
      amount: parseFloat(amount.value),
    }

    emit('transaccionEmitida',datosTransaccion);
    text.value = '';
    amount.value = '';
  }
</script>