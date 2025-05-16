<script setup>
import InputText from 'primevue/inputtext'
import DataTable from 'primevue/datatable'
import Column from 'primevue/column'
import Button from 'primevue/button';


import { ref } from 'vue'

const nombre = ref('')
const apellido = ref('')
const edad = ref('')
const genero = ref('')
const cedula = ref('')
const personas = ref([])
const personasRegistradas = ref([
       {
        id: 1,
        nombre: 'Jared',
        apellido: 'Ochoa',
        edad: 19,
        genero: 'Masculino',
        cedula: '0958899189'
      },
      {
        id: 2,
        nombre: 'Noelia',
        apellido: 'Ochoa',
        edad: 32,
        genero: 'Femenino',
        cedula: '0958745435'
      },
      {
        id: 3,
        nombre: 'Elena',
        apellido: 'Ochoa',
        edad: 28,
        genero: 'Femenino',
        cedula: '0954875843'
      }
])
personas.value.push(...personasRegistradas.value)
let idContador = Math.max(...personas.value.map(persona => persona.id), 0) + 1;
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

function eliminarPersona(id) {
    personas.value = personas.value.filter(persona => persona.id != id);
}

</script>

<template>
    <form class="form-container" >
        <div class="inputs-container">
            <InputText name="Nombre" type="text" v-model="nombre" placeholder="Nombre" />
            <InputText name="Apellido" type="text" v-model="apellido" placeholder="Apellido" />
            <InputText name="Edad" type="number" v-model="edad" placeholder="Edad" />
            <InputText name="Genero" type="text" v-model="genero" placeholder="Genero" />
            <InputText name="Cedula" type="text" v-model="cedula" placeholder="Cedula" />
        </div>
            <Button label="Guardar" @click="guardarDatos"/>
    </form>
    <DataTable class="card" :value="personas" :showGridlines="true" tableStyle="min-width: 50rem">
        <Column field="id" header="ID"></Column>
        <Column field="nombre" header="Nombre"></Column>
        <Column field="apellido" header="Apellido"></Column>
        <Column field="edad" header="Edad"></Column>
        <Column field="genero" header="Genero"></Column>
        <Column field="cedula" header="Cedula"></Column>
        <Column header="Acciones">
            <template #body="{ data }">
                <Button
                label="Eliminar"
                icon="pi pi-trash"
                outlined
                rounded
                severity="danger"
                @click="eliminarPersona(data.id)"/>
                <Button style="margin-left: 10px;"
                label="Editar"
                icon="pi pi-pencil"
                outlined
                rounded
                severity="secondary"
                @click="editarPersona(data.id)"/>
            </template>
        </Column>
    </DataTable>
</template>

<style scoped>
    .form-container{
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 3rem;
        gap: 1rem;
    }

    .form-container .inputs-container{
        display: flex;
        flex-direction: row;
        gap: 1rem;
    }

    .card {
        margin-top: 3rem;
    }
</style>
