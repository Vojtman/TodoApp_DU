<script setup>
import { ref, computed } from 'vue'
const newTask = ref('');
    const tasks = ref([
      { text: 'První úkol', isComplete: false },
      { text: 'Druhý úkol', isComplete: true },
    ]);

    const incompleteTaskCount = computed(() => {
      return tasks.value.filter(task => !task.isComplete).length;
    });

    function addTask() {
      if (newTask.value) {
        tasks.value.push({ text: newTask.value, isComplete: false });
        newTask.value = '';
      }
    }

    function removeTask(index) {
      tasks.value.splice(index, 1);
    }

    function toggleComplete(index) {
      tasks.value[index].isComplete = !tasks.value[index].isComplete;
    }

</script>

<template>
   <h1>Seznam úkolů</h1>
    <ul>
      <li v-for="(task, index) in tasks" :key="index" :class="{ 'is-complete': task.isComplete }">
        {{ task.text }}
        <button @click="() => toggleComplete(index)">Dokončit</button>
        <button @click="() => removeTask(index)">Odstranit</button>
      </li>
    </ul>
    <p>Počet nedokončených úkolů: {{ incompleteTaskCount }}</p>
    <input v-model="newTask" placeholder="Nový úkol">
    <button @click="addTask">Přidat úkol</button>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
