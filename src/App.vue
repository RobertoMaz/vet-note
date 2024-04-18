<script setup>
  import Header from './components/Header.vue'
  import Formulario from './components/Formulario.vue'
  import { ref , reactive} from 'vue'

  const patients = ref([])

  
  const patient = reactive({
        petName: '',
        owner: '',
        email:'',
        register:'',
        symptoms:''
    })


</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />
    <div class="mt-12 md:flex">
      <Formulario 
        v-model:petName="patient.petName"
        v-model:owner="patient.owner"
        v-model:email="patient.email"
        v-model:register="patient.register"
        v-model:symptoms="patient.symptoms"



      />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>
        <div v-if="patient.length > 0">
        
        </div>
        <p v-else class="mt-20 text-2xl text-center">No hay pacientes</p>
      </div>
    </div>
  </div>
</template>
