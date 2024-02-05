<template>
    <div class="inc-exp-container">
        <div>
            <h4>Saldo entrante</h4>
            <p id="money-plus" class="money plus text-red-600">
                +${{ income }}
            </p>
        </div>
        <div>
            <h4>Saldo de salida</h4>
            <p id="money-minus" class="money minus">-${{ expenses }}</p>
        </div>
    </div>
</template>

<script setup>

import { defineProps } from "vue";
const props = defineProps({
    income:{
        type: Number,
        required: true,
    },
    expenses:{
        type: Number,
        required: true,
    }
})
</script>