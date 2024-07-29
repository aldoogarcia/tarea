<script setup>
import { reactive } from 'vue';
import headerItem from '../components/header-item.vue';



    const form = reactive({
        nombre: '',
        fecha: '',
        descripcion: '',
        // categoria:'',
        // prioridad:false
    })

    const validarFormulario=()=>{
        const formComplete= Object.values(form).includes('');
        if(formComplete){
            alert('Todos los campos son obligatorios')
            
        }else{
            alert('Se Guardo.....')
        }
    }
</script>
<template>
    <headerItem/>
    <div class="md:w-1/2 mt-10 px-7" >

        <p class="text-xl text-center">Agrega Nueva <span class="text-green-600">Tarea</span></p>

        <form 
        @submit.prevent="validarFormulario"
        class="px-10 py-10 shadow-lg shadow-black-100">
            <div>
                <label class="uppercase block mt-3" for="nombre">Nombre Tarea</label>
                <input class="border-2 border-b-sky-300 border-spacing-10  w-full rounded-lg mt-1 placeholder-gray-400 placeholder-opacity-40" 
                id="nombre"
                type="text"
                placeholder="Ingresa el nombre de la tarea"
                v-model="form.nombre"
                >
            </div>

            <div>
                <label class="uppercase block mt-4" for="fecha">Fecha de vencimiento</label>
                <input 
                type="datetime-local" 
                id="fecha"
                class="w-full mt-1 border-2 border-b-sky-300  rounded-lg text-center"
                v-model="form.fecha"
                >
            </div>

            <div>
                <label class="uppercase block mt-4" for="descripcion">Descripcion</label>
                <textarea
                class="w-full mt-1 border-2 border-b-sky-300  rounded-lg"
                id="descripcion"
                placeholder="Descripcion de la tarea"
                v-model="form.descripcion"
                >

                </textarea>

            <div>
                <label class="uppercase block mt-3" for="categoria">Categoria</label>
                <select
                class="w-full mt-1 border-2 border-b-sky-300  rounded-lg text-center"
                id="categoria">
                    <option value="">-- Selecciona --</option>
                    <option value="Escuela">Escuela</option>
                    <option value="Escuela">Familia</option>
                    <option value="Escuela">Novia</option>
                </select>
            </div>

            <div class="mt-3">
                <label class="uppercase " for="prioridad">Prioridad</label>
              <input type="checkbox" id="prioridad" class="mx-3">
            </div>
                
            </div>
            
            <input 
            type="submit" 
            value="Guardar" 
            class="bg-blue-500 hover:bg-blue-700 cursor-pointer transition-colors w-full mt-3 rounded-lg text-white"
            >

        </form>


    </div>
</template>