<script setup>
import InputText from 'primevue/inputtext'
import Button from 'primevue/button'
import DataTable from 'primevue/datatable'
import Column from 'primevue/column'

import { ref } from 'vue'

const nombre = ref('')
const apellido = ref('')
const edad = ref('')
const genero = ref('')
const cedula = ref('')
const personas = ref([])
let idContador = 1;

function guardarDatos() {
    const nuevaPersona = {
        id: idContador++,
        nombre: nombre.value,
        apellido: apellido.value,
        edad: edad.value,
        genero: genero.value,
        cedula: cedula.value
    }
    personas.value.push(nuevaPersona)
}

</script>
<template>
    <form class="form-container" >
        <InputText name="Nombre" type="text" v-model="nombre" placeholder="Nombre" />
        <InputText name="Apellido" type="text" v-model="apellido" placeholder="Apellido" />
        <InputText name="Edad" type="number" v-model="edad" placeholder="Edad" />
        <InputText name="Genero" type="text" v-model="genero" placeholder="Genero" />
        <InputText name="Cedula" type="text" v-model="cedula" placeholder="Cedula" />
        <Button label="Guardar" @click="guardarDatos"/>
    </form>
    <DataTable class="card" :value="personas" :showGridlines="true" tableStyle="min-width: 50rem ">
        <Column field="id" header="ID"></Column>
        <Column field="nombre" header="Nombre"></Column>
        <Column field="apellido" header="Apellido"></Column>
        <Column field="edad" header="Edad"></Column>
        <Column field="genero" header="Genero"></Column>
        <Column field="cedula" header="Cedula"></Column>
    </DataTable>
</template>


<style scoped>
    .form-container{
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 1rem;

    }
    .card {
        margin: 10px;
    }

</style>
