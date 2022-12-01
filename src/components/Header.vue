<template>
  <header class="flex justify-between py-6 items-center ">
    <h1 class="font-bold text-2xl">{{ title }}</h1>
    <Button @btn-click="$emit('toggle-add-task')"
      :class="showAddTask ? ' bg-red-500 text-white p-2 rounded-md' : 'bg-green-500 text-white p-2 rounded-md'"
      :text="showAddTask ? 'Close' : 'Add Task'" />
  </header>
</template>


<script>
import Button from './Button.vue';

export default {
  name: "Header",

  components: {
    Button,
  },

  props: {
    title: String,
    showAddTask: Boolean,
  }
};
</script>
