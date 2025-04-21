<script setup lang="ts">
import { defineProps, defineEmits, ref } from 'vue'

const props = defineProps({
    task: {
        type: Object,
        required: true
    }
})

const emit = defineEmits(['editar', 'remover'])

const showModal = ref(false)

const titulo = ref(props.task.titulo)
const descricao = ref(props.task.descricao)
const status = ref(props.task.status)

const abrirModal = () => {
    titulo.value = props.task.titulo
    descricao.value = props.task.descricao
    status.value = props.task.status
    showModal.value = true
}

const editarTask = async () => {
    try {
        const res = await fetch(`http://localhost:8000/tasks/${props.task.id}`, {
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                titulo: titulo.value,
                descricao: descricao.value,
                status: status.value
            })
        })

        if (!res.ok) {
            throw new Error('Erro ao editar tarefa')
        }

        const taskAtualizada = await res.json()
        alert('Tarefa editada com sucesso!')
        emit('editar', taskAtualizada)
        showModal.value = false
    } catch (err) {
        console.error(err)
        alert('Erro ao editar a tarefa')
    }
}

const deletarTask = async () => {
    try {
        const res = await fetch(`http://localhost:8000/tasks/${props.task.id}`, {
            method: 'DELETE'
        })

        if (!res.ok) {
            throw new Error('Erro ao deletar tarefa')
        }

        alert('Tarefa deletada com sucesso!')
        emit('remover', props.task.id)
    } catch (err) {
        console.error(err)
        alert('Erro ao deletar a tarefa')
    }
}
</script>

<template>
    <div class="task-card">
        <h2>{{ task.titulo }}</h2>
        <p>{{ task.descricao }}</p>
        <p><strong>Status:</strong> {{ task.status }}</p>

        <div class="actions">
            <button @click="abrirModal">Editar</button>
            <button @click="deletarTask">Deletar</button>
        </div>

        <div v-if="showModal" class="modal-overlay">
            <div class="modal-content">
                <h3>Editar Tarefa</h3>
                <input type="text" v-model="titulo" placeholder="Título" />
                <textarea v-model="descricao" placeholder="Descrição"></textarea>
                <input type="text" v-model="status" placeholder="Status" />

                <div class="actions">
                    <button @click="editarTask">Salvar</button>
                    <button @click="showModal = false">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.task-card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 1rem;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #0000002a;
}

.actions {
    margin-top: 1rem;
    display: flex;
    justify-content: space-between;
    gap: 10px;
}

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

button:last-of-type {
    background-color: #ff5f5f;
    color: white;
}

.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.4);
    backdrop-filter: blur(6px);
    -webkit-backdrop-filter: blur(6px);

    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
}

.modal-content {
    min-width: 600px;
    max-width: 600px;
    border: 1px solid #0051ff;
    border-radius: 8px;
    padding: 1rem;
    margin: 1rem 0;
    background-color: #000000e6;
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
}
</style>
