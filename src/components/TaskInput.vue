<template>
  <div class="mb-4">
    <h1 class="text-4xl font-mono uppercase ">Todo List</h1>
    <div class="flex flex-col mt-4 w-full">
      <input v-model="title" placeholder="Title" type="text" class="shadow appearance-none border rounded w-full p-2 mb-2" />
      <input v-model="description" placeholder="Description" type="text"
        class="shadow appearance-none border rounded w-full p-2" />
    </div>
    <button @click="onAddTask" class="flex-no-shrink p-2 mt-3 border-2 rounded text-teal-500 border-teal-500">Add
      task</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  emits: {
    onAddTask({ title, description }) {
      if (title === '' || description === '') {
        alert('Fill some info please')
        return false;
      }
      return true;
    }
  },
  setup(props, { emit }) {
    const title = ref('')
    const description = ref('')

    const onAddTask = () => {
      emit('onAddTask', { title: title.value, description: description.value })
    }

    return {
      title,
      description,
      onAddTask
    }
  }
}
</script>

<style scoped>

</style>