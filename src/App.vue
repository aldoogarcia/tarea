<script setup>
import { reactive,ref } from 'vue';
import {uid} from 'uid'
   import formularioItem from './components/formulario-item.vue'
   import headerItem from './components/header-item.vue';
   import tareasItem from './components/tareas-item.vue';
import { watch } from 'vue';
import { onMounted } from 'vue';


   const tareas= ref([])

   const form = reactive({
        id:null,
        nombre: '',
        fecha: '',
        descripcion: '',
        categoria:'',
        prioridad:false
    })

    const guardarDatos = () => {
      // console.log('Validando....')
      //para quitar la reactividad
      if(form.id){
        const i= tareas.value.findIndex(existe => existe.id == form.id)
        tareas.value[i]={...form}
      }else{
        tareas.value.push(
         {
         ...form,
         id:uid()
        })
      }
        
       
      Object.assign(form,{
        id:null,
        nombre:'',
        fecha:'',
        descripcion:'',
        categoria:'',
        prioridad:false,
 
      })
    }


    const editarTarea= (id)=>{
      const tarea =tareas.value.filter(tarea => tarea.id==id); 
      Object.assign(form,... tarea);
      
    }

    const eliminarTarea=(id) => {
      // console.log("🚀 ~ eliminarTarea ~ id:", id)
      if(confirm("Deseas eliminar esta tarea")){
        tareas.value= tareas.value.filter(buscador => buscador.id != id)
      }

      
    }
    onMounted(()=>{
    const isTareas = localStorage.getItem('tarea')
    if(isTareas){
      tareas.value= JSON.parse(isTareas)
    }
    // tareas.value= localStorage.getItem('tarea')
  })

    watch(tareas,()=>{
      localStorage.setItem('tarea',JSON.stringify(tareas.value))

    },
  {
    deep: true,
  }
  )


    
</script>

<template>
   <headerItem/>
   <div class="md:flex ">
   <formularioItem
  v-model:id="form.id"
  v-model:nombre="form.nombre"
  v-model:fecha="form.fecha"
  v-model:descripcion="form.descripcion"
  v-model:categoria="form.categoria"
  v-model:prioridad="form.prioridad"
  @validar-form="guardarDatos"
  />

 <div class="md:w-1/2 mt-10 h-screen overflow-y-auto">
   <p class="text-2xl text-center">Pendientes</p>
   
   <tareasItem
   v-for="tarea in tareas"
   :key="tarea.nombre"
   :tarea="tarea"
   v-if="tareas.length>0"
   @editar-tarea="editarTarea"
   @eliminar-tarea="eliminarTarea"
   
   />
   <p v-else class="mt-10 text-center">No hay Pendientes</p>
 </div>
</div>
</template>

<style scoped>

</style>
