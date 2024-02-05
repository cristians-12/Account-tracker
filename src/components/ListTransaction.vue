<template>
  <div>
    <h3>Historial</h3>
    <ul id="list" class="list">
      <li
        v-for="transaction in transactions"
        :key="transaction.id"
        :class="transaction.amount < 0 ? 'minus' : 'plus'"
      >
        {{ transaction.text }} <span>${{ transaction.amount }}</span>
        <button class="delete-btn" @click="borrarTransaccion(transaction.id)" >x</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
  import { defineProps } from "vue";

  const props = defineProps({
    transactions:{
      type:Array,
      required: true,
    }
  }
  );
  
    const emit = defineEmits(["transaccionBorrada"])

    const usuarios = [

    ]

    const borrarTransaccion = (id)=>{
      emit ('transaccionBorrada',id)
    }
</script>