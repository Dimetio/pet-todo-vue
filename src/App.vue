<template>
  <main class="h-100 w-full flex items-center justify-center bg-teal-lightest font-sans">
    <div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
      <TaskInputVue @onAddTask="addTask"></TaskInputVue>
      <ul v-if="!empty">
        <li v-for="item in taskList" :key="item.id">
          <TaskCardVue :model="item" @onRemove="removeTask(item.id)" @onDone="setDoneTask(item.id)"></TaskCardVue>
        </li>
      </ul>
      <div v-else class="text-4xl">List is empty</div>
    </div>
  </main>
</template>


<script>
import TaskInputVue from './components/TaskInput.vue';
import TaskCardVue from './components/TaskCard.vue';
import { ref } from 'vue';

export default {
  name: 'App',
  components: {
    TaskCardVue,
    TaskInputVue
  },

  setup() {
    let empty = ref(false);
    const taskList = ref([{ id: 0, title: 'Learn TS', description: 'Rewrite project on TS', status: false }])

    const addTask = ({ title, description }) => {
      const lastItem =  taskList.value[taskList.value.length - 1];
      empty.value = false;

      taskList.value = [...taskList.value, { id: lastItem ? lastItem.id + 1 : 0, title, description, status: false }]
    }

    const setDoneTask = (id) => {
      taskList.value = taskList.value.map(x => {
        if (x.id === id) {
          x.status = true;
        }

        return x;
      })
    }

    const removeTask = (id) => {
      taskList.value = taskList.value.filter(x => x.id !== id);
      if (taskList.value.length === 0) {
        empty.value = true;
      }
    }

    return {
      taskList,
      addTask,
      setDoneTask,
      removeTask,
      empty,
    }
  }
}
</script>

<style scoped>
.task-list {
  list-style: none;
}
</style>
