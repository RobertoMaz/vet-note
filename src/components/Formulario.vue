<script setup>
    // import { ref } from 'vue'
    // const petName = ref('')

    import { reactive, computed } from 'vue'
    import AlertMessage from './AlertMessage.vue'

    const alertMessage = reactive({
        type: '',
        message: ''
    })

    const emit = defineEmits(['update:petName','update:owner','update:email','update:register','update:symptoms', 'save-patient'])

    const props = defineProps({
        id: {
            type: [String, null],
            required: true
        },
        petName: {
            type: String,
            required: true
        },
        owner: {
            type: String,
            required: true
        },
        email: {
            type: String,
            required: true
        },
        register: {
            type: String,
            required: true
        },
        symptoms: {
            type: String,
            required: true
        }
    })

    const edit = computed(() => {
        return props.id
    })


    const validateForm = () => {
        if(Object.values(props).includes('')){
            alertMessage.message = 'Todos los campos son obligatorios'
            alertMessage.type = "error"
            return
        }

        emit('save-patient')
        alertMessage.message = 'Pacientes almacenados correctamente'
        alertMessage.type = "exito"

        setTimeout(() => {
            Object.assign(alertMessage, {
                type: '',
                message: ''
            })
        }, 3000);
    }

</script>
<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento pacientes</h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade pacientes y
            <span class="text-indigo-600 font-bold">adminístralos</span>
        </p>
        <AlertMessage 
            v-if="alertMessage.message"
            :alertMessage="alertMessage"
        />
        <form
            class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
            @submit.prevent="validateForm"
        >
            <div class="mb-5">
                <label
                    for="pet"
                    class="block text-gray-700 uppercase font-bold"
                >Nombre Mascota
                </label>
                <input 
                    id="pet"
                    type="text"
                    placeholder="Nombre de la mascota"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="petName"
                    @input="$emit('update:petName', $event.target.value)"
                    />
                </div>
                <div class="mb-5">
                    <label
                        for="owner"
                        class="block text-gray-700 uppercase font-bold"
                    >Nombre Propietario
                </label>
                <input 
                    id="owner"
                    type="text"
                    placeholder="Nombre del propietario"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="owner"
                    @input="$emit('update:owner', $event.target.value)"
                />
            </div>
            <div class="mb-5">
                <label
                    for="email"
                    class="block text-gray-700 uppercase font-bold"
                >Email
                </label>
                <input 
                    id="email"
                    type="email"
                    placeholder="Email del propietario"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="email"
                    @input="$emit('update:email', $event.target.value)"
                />
            </div>
            <div class="mb-5">
                <label
                    for="register"
                    class="block text-gray-700 uppercase font-bold"
                >Alta
                </label>
                <input 
                    id="register"
                    type="date"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="register"
                    @input="$emit('update:register', $event.target.value)"
                />
            </div>
            <div class="mb-5">
                <label
                    for="symptoms"
                    class="block text-gray-700 uppercase font-bold"
                >Síntomas
                </label>
                <textarea
                    id="symptoms"
                    placeholder="Describe los Síntomas"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-40"
                    :value="symptoms"
                    @input="$emit('update:symptoms', $event.target.value)"
                />
            </div>
            <input 
                type="submit"
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold
                 hover:bg-indigo-700 cursor-pointer transition-colors
                 rounded-md"
                 :value="[edit ? 'Guardar Cambios': 'Registrar paciente']"
            />
        </form>
    </div>
</template>
