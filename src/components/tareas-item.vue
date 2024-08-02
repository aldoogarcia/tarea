<script setup>


    const emit= defineEmits(['editar-tarea','eliminar-tarea'])
    const props =defineProps({
        tarea:{
            type:Object,
            required: true
        }
    })  
        
        
    const editTarea=()=>{
        emit('editar-tarea',props.tarea.id)
    }

    const eliminarTarea= ()=>{
        emit('eliminar-tarea',props.tarea.id)
    }

</script>
<template>
    <div 
    :class="[props.tarea.prioridad ? 'border-2 border-red-500': 'bg-white']"
    class="mx-5 my-10 shadow-md px-5 py-10 rounded-xl">
        <p class="font-bold mb-3 text-gray-700 uppercase " v-if="false">ID:
            <span class="font-normal normal-case">
                {{ props.tarea.id  }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Nombre:
            <span class="font-normal normal-case">
                {{ tarea.nombre }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Descripcion: 
            <span class="font-normal normal-case">
                {{ tarea.descripcion }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Fecha Entrega: 
            <span class=" px-1 font-normal normal-case">
                {{tarea.fecha }}
            </span>
        </p>
        <!-- <p class="font-bold mb-3 text-gray-700 uppercase">Hora de Entrega: 
            <span class="border-1 bg-gray-400 px-1 font-normal normal-case">
                {{tarea.fecha }} {{ 'am' }}
            </span>
        </p> -->

        <p class="font-bold mb-3 text-gray-700 uppercase">Categoria:
            <span class="font-normal normal-case">
                {{ tarea.categoria }}
            </span>
        </p>

        <div class="grid md:grid-cols-2  gap-5 mt-10 ">
            <button 
                @click="editTarea"
                type="button"
                class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg"
            >Editar</button>

            <button 
                @click="eliminarTarea"
                type="button"
                class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg"
            >Eliminar</button>
        </div>
    </div>
</template>