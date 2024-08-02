<script setup>
import { reactive } from 'vue';
import alertaItem from './alerta-item.vue';


    const alerta= reactive({
        tipo:'',
        mensaje:''
    })

    
    const emit = defineEmits(['update:nombre', 'update:fecha','update:descripcion','update:categoria','update:prioridad','update:id','validar-form'])

    const props = defineProps({
        id:{
            type: String,
        },
        nombre:{
            type:String,
            required: true
        },
        fecha:{
            type:String,
            required: true
        },
        descripcion:{
            type:String,
            required: true
        },
        categoria:{
            type:String,
            required: true
        },
        prioridad:{
            type:Boolean,
            
            
        }
    })





    const validarFormulario=()=>{
        const formComplete= Object.values(props).includes('');
        if(formComplete){
            alerta.tipo='error'
            alerta.mensaje='Todos los campos son obligatorios'
           return
            
        }else{
            alerta.tipo='exito'
            alerta.mensaje='Tarea Guardada'
            emit('validar-form')
        }

        setTimeout(()=>{
            alerta.tipo=''
            alerta.mensaje=''
        }, 5000)

    }
</script>
<template>
    
    <div class="md:w-1/2 mt-10 px-7" >

        <p class="text-xl text-center">Agrega Nueva <span class="text-green-600">Tarea</span></p>
        <alertaItem
        v-if="alerta.tipo"
        :alerta="alerta"
        />
        <form 
        @submit.prevent="validarFormulario"
        class="px-10 py-10 shadow-lg shadow-black-100">
            <div>
                <label class="uppercase block mt-3" for="nombre">Nombre Tarea</label>
                <input class="border-2 border-b-sky-300 border-spacing-10  w-full rounded-lg mt-1 placeholder-gray-400 placeholder-opacity-40" 
                id="nombre"
                type="text"
                placeholder="Ingresa el nombre de la tarea"
                :value="nombre"
                @input="$emit('update:nombre',$event.target.value)"
                >
            </div>

            <div>
                <label class="uppercase block mt-4" for="fecha">Fecha de vencimiento</label>
                <input 
                type="datetime-local" 
                id="fecha"
                class="w-full mt-1 border-2 border-b-sky-300  rounded-lg text-center"
                @input="$emit('update:fecha',$event.target.value)"
                :value="fecha"
                >
            </div>

            <div>
                <label class="uppercase block mt-4" for="descripcion">Descripcion</label>
                <textarea
                class="w-full mt-1 border-2 border-b-sky-300  rounded-lg"
                id="descripcion"
                :value="descripcion"
                placeholder="Descripcion de la tarea"
                @input="$emit('update:descripcion',$event.target.value)"
                >

                </textarea>

            <div>
                <label class="uppercase block mt-3" for="categoria">Categoria</label>
                <select
                :value="categoria"
                @input="$emit('update:categoria',$event.target.value)"
                class="w-full mt-1 border-2 border-b-sky-300  rounded-lg text-center"
                id="categoria">
                    <option value="">-- Selecciona --</option>
                    <option value="Escuela">Escuela</option>
                    <option value="Familia">Familia</option>
                    <option value="Novia">Novia</option>
                </select>
            </div>

            <div class="mt-3">
                <label class="uppercase " for="prioridad">Prioridad</label>
              <input
              :value="prioridad"
              @input="$emit('update:prioridad',$event.target.checked)" type="checkbox" id="prioridad" class="mx-3">
            </div>
                
            </div>
            
            <input 
            type="submit" 
            :value="[props.id==null ? 'Guardar Datos' : 'Actualizar Datos']" 
            class="bg-blue-500 hover:bg-blue-700 cursor-pointer transition-colors w-full mt-3 rounded-lg text-white"
            >

        </form>


    </div>
</template>