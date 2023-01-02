
<script setup>

defineProps(['start', 'end', 'total']);
const emit = defineEmits(['next', 'previus']);

</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button @click="emit('previus')" :disabled="start <= 0" type="button" class="btn btn-outline-primary">Previus</button>
        <button @click="emit('next')" :disabled="end >= total" type="button" class="btn btn-outline-primary">Next</button>
    </div>
</template>