<script>
export default {
    name: 'CarPaciente',
    props: {
        paciente: {
            type: Object,
            Required: true
        }
    },
    methods: {
        eliminarPaciente() {
            this.$emit('eliminar', this.paciente)
        }
    }
}
</script>
<template>

    <!-- se crean las card para cada registro -->
    <div class="card" :style="{
        backgroundColor: paciente.valueGravedad === 'Baja' ? 'green' :
            paciente.valueGravedad === 'Media' ? 'yellow' : 'red'
    }">
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
            <button @click.prevent="eliminarPaciente">Eliminar</button>
        </div>
    </div>
</template>
<style scoped>
.card {
    display: flex;
    flex-direction: column;
    width: 10rem;
    padding: 1rem;
    text-align: center;
    gap: 1rem;
    margin-top: 2rem;
    border-radius: 10px;
}
</style>