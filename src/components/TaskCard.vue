<template>
  <div class="flex mb-4 items-center border-b-2">
    <div class="w-full">
      <h4 class="mb-2 text-2xl">{{model.title}}</h4>
      <p class="mb-2">{{model.description}}</p>
    </div>
    <div>
      <button @click="emitOnDone" v-if="!model.status" class="p-2 border-2 border-green-500 rounded text-green-500">Done</button>
      <button @click="emitOnRemove" v-else class="p-2 border-2 border-red-500 text-red-500 rounded">Remove</button>
    </div>
  </div>
</template>

<script>
export default {
  emits: ['onDone', 'onRemove'],
  props: {
    model: {
      required: true,
      default: {
        id: 0,
        title: 'Default title',
        description: 'Default description',
        status: false
      }
    }
  },
  setup(props, { emit }) {
    const emitOnDone = () => {
      emit('onDone')
    }

    const emitOnRemove = () => {
      emit('onRemove')
    }

    return {
      emitOnDone,
      emitOnRemove
    }
  }
}
</script>

<style scoped>
</style>