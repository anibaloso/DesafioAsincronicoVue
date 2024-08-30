<script>
export default {
    name: 'CitaMedica',
    data() {
        return {
            pacientes: {
                paciente: '',
                fecha: '',
                hora: '',
                gravedad: ['Baja', 'Media', 'Alta'],
                valueGravedad: '',
                motivo: '',
            },
            listaPacientes: []
        }
    },
    methods: {
        agregarPacientes() {
            const nuevoPaciente = this.pacientes;
            this.listaPacientes.push(nuevoPaciente)
            this.pacientes = {
                paciente: '',
                fecha: '',
                hora: '',
                gravedad: ['Baja', 'Media', 'Alta'],
                valueGravedad: '',
                motivo: '',
            }
        },
        eliminarPaciente(idx){
            this.listaPacientes.splice(idx,1)
        }
    }
}
</script>

<template>
    <div class="container">
        <div class="ficha">
            <div class="column">
                <label :style="{ color: pacientes.paciente === '' ? 'red' : 'black' }">Paciente</label>
                <input type="text" v-model="pacientes.paciente">
            </div>
            <div class="column">
                <label :style="{ color: pacientes.fecha === '' ? 'red' : 'black' }">Fecha</label>
                <input type="date" v-model="pacientes.fecha">
            </div>
            <div class="column">
                <label :style="{ color: pacientes.hora === '' ? 'red' : 'black' }">Hora</label>
                <input type="time" v-model="pacientes.hora">
            </div>
            <div class="column">
                <label :style="{ color: pacientes.valueGravedad === '' ? 'red' : 'black' }">Gravedad</label>
                <select v-model="pacientes.valueGravedad">
                    <option v-for="(estado, idx) in pacientes.gravedad" :key="idx" :value="estado">{{ estado }}</option>
                </select>
            </div>
            <div class="column">
                <label :style="{ color: pacientes.motivo === '' ? 'red' : 'black' }">Motivo</label>
                <input type="text" v-model="pacientes.motivo">
            </div>
        </div>

        <div>
            <button @click.prevent="agregarPacientes" 
            :disabled="!pacientes.paciente || 
            !pacientes.fecha || 
            !pacientes.hora || 
            !pacientes.valueGravedad || 
            !pacientes.motivo "
            >Agregar</button>
        </div>
    </div>

    <!-- se crean las card para cada registro -->
    <div class="cards">
        <div class="card" 
        :style="{backgroundColor: paciente.valueGravedad === 'Baja' ? 'green' : 
        paciente.valueGravedad ==='Media' ? 'yellow' : 
        paciente.valueGravedad === 'Alta' ? 'red' : 'white' }"
        v-for="(paciente, idx) in listaPacientes" :key="idx">
            <div class="column">
                <label><strong>Paciente</strong> </label>
                <p>{{ paciente.paciente }}</p>
            </div>
            <div class="column">
                <label><strong>Fecha</strong> </label>
                <p>{{ paciente.fecha }}</p>
            </div>
            <div class="column">
                <label><strong>Hora</strong> </label>
                <p>{{ paciente.hora }}</p>
            </div>
            <div class="column">
                <label><strong>Motivo</strong> </label>
                <p>{{ paciente.motivo }}</p>
            </div>
            <div class="column">
                <button @click.prevent="eliminarPaciente(idx)">Eliminar</button>
            </div>
        </div>
    </div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    border: 1px solid black;
    border-radius: 5;
    padding: 1.5rem;

    text-align: center;
}

.ficha {
    display: flex;
    justify-content: space-around;
    margin-bottom: 2rem;
}

.column {
    display: flex;
    flex-direction: column;
}

.card {
    display: flex;
    flex-direction: column;
    width: 10rem;
    padding: 1rem;
    text-align: center;
    gap: 1rem;
}

.cards {
    display: flex;
    flex-direction: row;
}
</style>
