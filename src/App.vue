<template>
    <div>
        <h1>Lista de Tarefas</h1>
        <hr>

        <!-- Insert tasks -->
        <form action="#" onsubmit="event.preventDefault()">
            <label for="description">Descrição:</label>
            <!-- v-model para vincular uma variável no script -->
            <input type="text" id="description" v-model="todo">
            <button type="submit" @click="addTodo(todo)">Inserir ➕</button>
            <button type="reset">Limpar 🧼</button>
        </form>
        
        <!-- Show tasks -->
        <div>
            <div v-for="obj in todoList" :key="obj.id">
                {{ obj.description }}
                <select v-model="obj.status">
                    <option value="doing">A fazer</option>
                    <option value="todo">Fazendo</option>
                    <option value="done">Feito</option>
                </select>
                <button @click="removeTodo(todo)">Excluir 🗑</button>
            </div>
            <p>Total: {{ total }} </p>
        </div>

    </div>
</template>

<script setup>
import { computed, ref } from 'vue';

const todo = ref("")

const todoList = ref([
    {
        id: 1,
        description: "Estudar Vue.js",
        status: "todo"
    },
    {
        id: 2,
        description: "Estudar React.js",
        status: "done"
    },
    {
        id: 3,
        description: "Estudar Angular.js",
        status: "doing"
    },
])

let lastId = 3;

const addTodo = (desc)=>{
    lastId++
    todoList.value.push({
        id: lastId,
        description: desc,
        status: "todo"
    })
}

const removeTodo = (todo)=>{
    let index = todoList.value.findIndex((item)=>{
        return item.id == todo.id
    })
    todoList.value.splice(index, 1)
}

const total = computed(()=>{
    return todoList.value.length
})

</script>

<style scoped>
    *{
        font-family: sans-serif;
    }
</style>
