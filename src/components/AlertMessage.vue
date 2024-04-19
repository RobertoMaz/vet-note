<script setup>
    import { computed } from 'vue'

    const props = defineProps({
        alertMessage: {
            type: Object,
            Required: true
        }
    })
  
    const isError = computed(() => {
        return props.alertMessage.type === "error"
    })

</script>

<template>
    <div 
        :class="[isError ? 'bg-red-500' : 'bg-green-500']"
        class="text-white text-center p-3 uppercase font-bold mb-3 rounded-md"
    >
        {{ alertMessage.message }}
    </div>
</template>

