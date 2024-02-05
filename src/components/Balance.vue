<template>
    <div>
        <h4>Mi balance</h4>
        <h1 id="id">${{ total }}</h1>
    </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
    total:{
        type: Number,
        required: true,
    }
})

</script>