<template>
  <div>
    <img class="logo" alt="Vue logo" src="../assets/logo.png">
    <div class="todo-app ">
      <p>Usando conceito basico, com conceitos de reatividade básica</p>
      <div class="task-input">
        <input v-model="novaTarefa" @keyup.enter="adicionarTarefa" placeholder="Adicione uma nova tarefa">
        <button @click="adicionarTarefa">Adicionar no To Do</button>
      </div>

      <!-- Renderização das demais tarefas -->
      <ul class="task-list">
        <li v-for="(tarefa, index) in tarefa" :key="index" class="task-item">
          {{ tarefa }}
          <button @click="removeTarefa(index)" class="remove-button">Remover</button>
        </li>


      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld', 

  data() {
    return {
      novaTarefa: '',                       /* Armazena o texto da nova tarefa que é inserida */
      tarefa: [],                           /* Mostra a lista de tarefas adicionadas */
    };
  },

  methods: {                                /* Define as funções que vão ser usados no componente */
              

    adicionarTarefa() {                     /* Funçao que ve se o campo de novaTarefa não está vazio ou com espaços desnecessarios */
      
      if (this.novaTarefa.trim() !== '') {  /* Adiciona a nova tarefa à lista de tarefas */
        this.tarefa.push(this.novaTarefa);  /* Limpa o campo de entrada (novaTarefa) após adicionar a tarefa */
        this.novaTarefa = '';
      }
    },

    removeTarefa(index) {                   
      this.tarefa.splice(index, 1);         /* Remove uma tarefa específica da lista com base no índice */
    },
  },
};
</script>

<style scoped>
.logo{
  max-width: 100px;
}

p{
  color: #fff;
}

.todo-app {
  max-width: 400px;
  margin: 20px auto;
  padding: 20px;
  background: #242323;
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
  color: rgb(255, 255, 255);
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
  color: #388E3C;
}

.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #d6c596;
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
