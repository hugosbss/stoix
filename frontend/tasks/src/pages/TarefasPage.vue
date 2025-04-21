<script setup lang="ts">
import { ref, onMounted } from 'vue'
import Card from '../components/Card.vue'
import Criar from '../components/Criar.vue'

interface Task {
    id: number
    titulo: string
    descricao: string
    status: string
}

const tasks = ref<Task[]>([])
const mostrarCriar = ref(false)

const carregarTasks = async () => {
    const response = await fetch('http://localhost:8000/tasks')
    tasks.value = await response.json()
}

onMounted(carregarTasks)

const adicionarTask = async () => {
    await carregarTasks()
    mostrarCriar.value = false
}

const editarTask = async (taskEditada: Task) => {
    try {
        await fetch(`http://localhost:8000/tasks/${taskEditada.id}`, {
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(taskEditada)
        })

        await carregarTasks()
    } catch (error) {
        console.error('Erro ao editar a tarefa:', error)
        alert('Erro ao editar a tarefa.')
    }
}

const removerTask = (id: number) => {
    tasks.value = tasks.value.filter((task) => task.id !== id)
}
</script>

<template>

    <div class="container">

        <button @click="mostrarCriar = !mostrarCriar">
            {{ mostrarCriar ? 'Fechar formulário ✖️' : 'Criar tarefa ➕' }}
        </button>

        <Criar v-if="mostrarCriar" :task="{ titulo: '', descricao: '', status: '' }" @criar="adicionarTask"
            @cancelar="mostrarCriar = false" />

        <div class="card">
            <div v-for="task in tasks" :key="task.id" style="width: 300px; height: 300%;">
                <Card :task="task" @remover="removerTask" @editar="editarTask" />
            </div>
        </div>
    </div>
</template>

<style scoped>
button {
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

button:first-of-type {
    background-color: #42b983;
    color: white;
}

.card {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 1rem;
    margin-left: 10%;
    margin-right: 10%;
}

.container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1rem;
}
</style>