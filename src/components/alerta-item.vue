<script setup>
import { computed } from 'vue';

        const props = defineProps({
            alerta:{
                type: Object,
                required: true
            }
        })

        const isError= computed(()=>{
            return props.alerta.tipo=='error'
            
        })
</script>

<template>
    
    <div 

    :class="[isError ? 'bg-red-600' : 'bg-green-600']"
    class="py-3 my-2">
        <p class="text-center text-white">{{ props.alerta.mensaje }}</p>
    </div>
</template>


