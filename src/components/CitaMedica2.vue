<script>
import CardPaciente from './CardPaciente.vue';



export default {
    name: 'CitaMedica',
    components:{
        CardPaciente
    },
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
            const nuevoPaciente = { ...this.pacientes};
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
        eliminarPaciente(paciente) {
            this.listaPacientes = this.listaPacientes.filter(p => p !== paciente);
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
    <div v-show="listaPacientes.length === 0 " :style="{textAlign:'center', color:'red'}" >
        Aún no hay consultas registradas 
    </div>
    <div class="cards">
        <CardPaciente
            v-for="(paciente,idx) in listaPacientes" 
            :key=idx 
            :paciente="paciente"
            @eliminar="eliminarPaciente"
            />
            
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


.cards {
    display: flex;
    flex-direction: row;
}
</style>
