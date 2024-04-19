<script setup>
  import { ref , reactive} from 'vue'
  import Header from './components/Header.vue'
  import Formulario from './components/Formulario.vue'
  import Patient from './components/Patient.vue'

  const patients = ref([])

  
  const patient = reactive({
      id: null,
      petName: '',
      owner: '',
      email:'',
      register:'',
      symptoms:''
    })

    const savePatient = () => {
      patients.value.push({
         ...patient,
         id: self.crypto.randomUUID()
        })

      patient.petName = ''
      patient.owner = ''
      patient.email = ''
      patient.register = ''
      patient.symptoms = ''
    }

    const updatePatient = () => {
      console.log("Estoy haciendo el update")
    }

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
        @save-patient="savePatient"


      />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>
        <div v-if="patients.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Información de 
            <span class="text-indigo-600 font-bold">Pacientes</span>
          </p>
          <Patient 
            v-for="patient in patients"
            :patient="patient"
            @update-patient="updatePatient"
          />
        </div>
        <p v-else class="mt-20 text-2xl text-center">No hay pacientes</p>
      </div>
    </div>
  </div>
</template>
