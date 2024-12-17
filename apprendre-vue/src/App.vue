<style>
.terminer {
  color: darkgreen;
  opacity: 0.5;
  text-decoration: line-through;
}

li:hover {
  cursor: pointer;
}
</style>

<template>
  <main class="container">
    <h2 class="mt-2">TODO LIST</h2>


    <form action="" @submit.prevent="addTask" class="mt-3">
      <div class="mb-3">
        <label for="inputTask" class="form-label">Ajouter une tâche</label>
        <input type="text" class="form-control" id="inputTask" aria-describedby="inputTask" v-model="task">
      </div>
      <button class="btn btn-primary" :disabled="task.length === 0">Ajouter</button>
    </form>
    <section v-if="todos.length === 0">
      <h3>pas de tache ne cours</h3>
    </section>

    <section class="mt-3" v-else="todos.length !== 0">
      <h3>Mes tâches</h3>
      <select class="form-select" aria-label="select todolist" @change="sortedTodo">
        <option selected value="1">toutes les tâches</option>
        <option value="2">à faire</option>
        <option value="3">terminer</option>
      </select>

      <ul class="list-group" v-for="todo in todos">
        <li class="list-group-item d-flex align-items-center" v-if="todo.completed===false" :key="todo.id">
          <div class="form-check">
            <label :class="{ terminer: todo.completed }">
              <input type="checkbox" v-model="todo.completed" @click="replaceTodo">
              {{ todo.name }}
            </label>
          </div>
          <button @click="deleteTask" class="btn btn-outline-primary ms-auto">supprimer</button>
        </li>
      </ul>
      <ul class="list-group" v-for="todo in todos">
        <li class="list-group-item d-flex align-items-center" v-if="todo.completed===true" :key="todo.id">
          <div class="form-check">
            <label :class="{ terminer: todo.completed }">
              <input type="checkbox" v-model="todo.completed" @click="replaceTodo">
              {{ todo.name }}
            </label>
          </div>
          <button @click="deleteTask" class="btn btn-outline-primary ms-auto">supprimer</button>
        </li>
      </ul>

    </section>
  </main>
</template>

<script setup>

import { ref } from 'vue'

// tableau des tache a faire
const todos = ref([
 /* {
    name: "une tache",
    completed: true,
    id: 1
  },
  {
    name: "une 2e tache",
    completed: true,
    id: 2
  },
  {
    name: "une 3e tache",
    completed: false,
    id: 3
  },
  {
    name: "une 4e tache",
    completed: false,
    id: 4
  },
  {
    name: "une 5e tache",
    completed: false,
    id: 5
  }*/
]);

// la nouvelle tache
const task = ref('');

// ajoute une tache au tableau todos
const addTask = () => {
  todos.value.push({
    name: task.value,
    completed: false,
    id: Date.now()
  });

  task.value = '';
}

const sortedTodo = () => {
  
}

// supprime un tache
const deleteTask = (e) => {
  e.target.parentElement.remove()
}

</script>
