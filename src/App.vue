
<template>
  <main>
    <!--heading-->
    <header>
      <img src="./assets/pinia-logo.svg" alt="logo" />
      <h1>Pinia Task</h1>
    </header>
    <div class="new-task-form">
      <TaskForm />

    </div>
    <!--filter-->
    <nav class="filter">
      <button @click="filter = 'all'">All Task</button>
      <button @click="filter = 'favs'">All Favorite</button>
    </nav>
    <!--loading-->
    <div class="loading" v-if="taskStore.loading">Loading tasks...</div>
    <!--task list-->
    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ taskStore.totalCount }} tasks left to do</p>
      <div v-for="task in taskStore.tasks">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ taskStore.favCount }} tasks left to do</p>
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
import TaskForm from './components/TaskForm.vue';
export default {
  components: {
    TaskDetails,
    TaskForm
  },
  setup() {
    const taskStore = useTaskStore();
    //fetch
    taskStore.getTasks()
    const filter = ref('all')

    return { taskStore, filter }
  }
}
</script>
