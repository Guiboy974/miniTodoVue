<style>
.terminer {
  opacity: 0.5;
  text-decoration: line-through;
}

li:hover {
  cursor: pointer;
}

</style>

<template>
  <main class="container">
    <h2 class="mt-2 text-center">TODO LIST</h2>

    <form action="" @submit.prevent="addTask" class="mt-3">
      <div class="mb-3 input-group">
        <input type="text" class="form-control" id="inputTask" aria-describedby="inputTask" v-model="task"
          placeholder="nouvelle tâche">
        <button class="btn btn-outline-warning" :disabled="task.length === 0">Ajouter</button>
      </div>
    </form>
    <section class="mt-3 text-center" v-if="todos.length === 0">
      <h3>pas de tâches en cours</h3>
    </section>
    <section class="mt-3" v-else="todos.length > 0">
      <ul class="list-group bg-transparent">
        <li class="list-group-item d-flex align-items-center text-white" v-for="todo in sortedTodo" :key="todo.id" style="background: transparent !important;">
          <div class="form-check">
            <label :class="{ terminer: todo.completed }">
              <input class="form-check-input" type="checkbox" v-model="todo.completed" @click="replaceTodo">
              {{ todo.name }}
            </label>
          </div>
          <button @click="deleteTask" class="btn btn-warning ms-auto">supprimer</button>
        </li>
      </ul>
      <div class="form-check mt-2">
        <label class="form-check-label" for="flexCheckDefault"><input class="form-check-input" type="checkbox" v-model="hideCompleted">
          Masquer les tâches terminer
        </label>
      </div>
    </section>
  </main>
</template>

<script setup>

import { computed, ref } from 'vue'

// tableau des tache a faire
const todos = ref([]);

// la nouvelle tache
const task = ref('');

// masque les tâches terminer
const hideCompleted = ref(false)

// ajoute une tache au tableau todos
const addTask = () => {
  todos.value.push({
    name: task.value,
    completed: false,
    id: Date.now()
  });

  task.value = '';
}

const sortedTodo = computed(() => {
  const sortedTodo = todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)

  if (hideCompleted.value === true) {
    return sortedTodo.filter(t => t.completed === false)
  }
  console.log(hideCompleted);
  
  return sortedTodo
})

// supprime un tache
const deleteTask = (e) => {
  return todos.value.splice(e.target.parentElement, 1)
}

</script>
