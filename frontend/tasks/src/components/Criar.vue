<script setup lang="ts">
import { defineProps, defineEmits, reactive } from 'vue'

const props = defineProps({
    task: {
        type: Object,
        required: true
    }
})

const emit = defineEmits(['criar'])

const form = reactive({
    titulo: props.task.titulo,
    descricao: props.task.descricao,
    status: props.task.status
})

const criarTask = async () => {
    try {
        const res = await fetch('http://localhost:8000/tasks', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(form)
        })

        if (!res.ok) {
            throw new Error('Erro ao criar tarefa')
        }

        const novaTask = await res.json()
        alert('Tarefa criada com sucesso!')
        emit('criar', novaTask)
    } catch (err) {
        console.error(err)
        alert('Erro ao criar a tarefa')
    }
}

</script>

<template>
    <div class="create-card">
        <input type="text" v-model="form.titulo" placeholder="Título" required />
        <textarea v-model="form.descricao" placeholder="Descrição" required></textarea>
        <textarea v-model="form.status" placeholder="Status" required></textarea>

        <div class="actions">
            <button @click="criarTask">Criar</button>
            <button @click="$emit('cancelar')">Cancelar</button>
        </div>
    </div>
</template>

<style scoped>
.create-card {
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 1rem;
    margin: 1rem 0;
    background-color: #0000002a;
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
}

.actions {
    margin-top: 1rem;
    margin-right: 50px;
    margin-left: 50px;
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
</style>