
<template>
  <main>
    <!--heading-->
    <header>
      <img src="./assets/pinia-logo.svg" alt="logo" />
      <h1>Pinia Task</h1>
    </header>
    <!--filter-->
    <nav class="filter">
      <button @click="filter = 'all'">All Task</button>
      <button @click="filter = 'favs'">All Favorite</button>
    </nav>
    <!--task list-->
    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{taskStore.totalCount }} tasks left to do</p>
      <div v-for="task in taskStore.tasks">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{taskStore.favCount }} tasks left to do</p>
      <div v-for="task in taskStore.favs">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<script>
import { useTaskStore } from './stores/TaskStore';
import TaskDetails from './components/TaskDetails.vue'
import { ref } from 'vue';
export default {
  components: {
    TaskDetails
  },
  setup() {
    const taskStore = useTaskStore();
    const filter = ref('all')

    return { taskStore, filter }
  }
}
</script>
