<template>
  <div>
    <input type="text" v-model="editedTask.name" />
    <input type="number" v-model.number="editedTask.time" />
    <button @click="submitEdit">Submit</button>
    <button @click="closePopup">Cancel</button>
  </div>
</template>

<script setup>
import { ref, defineProps } from 'vue';

const props = defineProps({
  task: {
    type: Object,
    required: true
  },
  onSubmit: {
    type: Function,
    required: true
  },
  onClose: {
    type: Function,
    required: true
  }
});

const editedTask = ref({ ...props.task });

const submitEdit = () => {
  props.onSubmit(editedTask.value);
};

const closePopup = () => {
  props.onClose();
};
</script>
