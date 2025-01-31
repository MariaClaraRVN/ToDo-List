<template>
    <div>
        <div class="todo-app ">
            <p>Usando um conceito intermediario que usa do gerenciamento de reatividade</p>
            <div class="task-input">
                <input v-model="newTask" @keyup.enter="addTask" placeholder="Adicione uma nova tarefa">
                <button @click="addTask">Adicionar no To Do</button>
            </div>

            <!-- Renderização das demais tarefas -->
             <ul class="task-list">
                <li v-for="(task, index) in tasks" :key="index" class="task-item">
                    {{ task }}
                    <button @click="removeTask(index)" class="remove-button">Remover</button>  
                </li>

                
             </ul>
        </div>
    </div>
</template>

<script>
import { ref } from 'vue'

export default {
    name: 'TodoList',
    setup() {                                           /* Serve para declaras as funções de forma reativa */
        const newTask = ref('')                         /* O termo 'ref', faz criar as variaveis reativas, ou seja, sempre que o valor da variavel MutationRecord, é atualizado automaticamente o DOM */
        const tasks = ref([])                           /* newTask é o valor da variavel reativa e a reatividade é usada em `v-model="newTask"` para atualizar na interface */

        const addTask = () => {                         /* Função que verifica o valor de 'newTask' */ 
            if (newTask.value.trim() !== '') {          /* Para remover espaços desnecessarios usa-se o 'trim()' */
                tasks.value.push(newTask.value)         /* Adiciona a nova tarefa (newTask) */
                newTask.value = ''                      /*na lista de tarefas (tasks.value) */
            }
        }

        const removeTask = (index) => {                 /* Função que vai deixar remover uma tarefa */ 
                tasks.value.splice(index, 1)            /* Remove uma tarefa com base no indice que foi utilizado como um parametro que seria o (spice) */
            }
        return { newTask, tasks, addTask, removeTask }  /* Retorna as variaveis para que possam ser exibidas no template */
        }
   }
</script>

<style scoped>
p{
  color: #000000;
}

.todo-app {
    max-width: 400px;
    margin: 20px auto;
    padding: 20px;
    background: #c2c1c1;
    border-radius: 10px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

/* Campo de entrada e botão */
.task-input {
    display: flex;
    gap: 10px;
    margin-bottom: 15px;
}

.task-input input {
    flex: 1;
    padding: 10px;
    font-size: 16px;
    border: 2px solid #ddd;
    border-radius: 5px;
    outline: none;
    transition: 0.3s;
}

.task-input input:focus {
    border-color: #4CAF50;
}

.task-input button {
    padding: 10px 15px;
    font-size: 14px;
    background: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: 0.3s;
}

.task-input button:hover {
    background: #388E3C;
}

/* Lista de tarefas */
.task-list {
    list-style: none;
    padding: 0;
}

.task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #f8f8f8;
    padding: 10px;
    margin: 5px 0;
    border-radius: 5px;
    font-size: 16px;
    transition: 0.3s;
}

.task-item:hover {
    background: #e0e0e0;
}

/* Botão de remoção */
.remove-button {
    background: #E53935;
    color: white;
    border: none;
    padding: 5px 10px;
    font-size: 12px;
    border-radius: 5px;
    cursor: pointer;
    transition: 0.3s;
}

.remove-button:hover {
    background: #C62828;
}
</style>