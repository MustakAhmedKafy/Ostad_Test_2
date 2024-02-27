<!-- TaskList.vue -->
<template>
  <div class="container pt-5 mt-5">
    <div v-for="(task, index) in tasks" :key="index" class="mb-3">
      <div class="h4">{{ task.name }}</div>
      <div class="h6">{{ task.time }}</div>
      <button @click="editTask(index)" class="btn btn-warning px-5">Edit</button>
    </div>
    <div v-if="showPopup" class="modal fade show mt-5 pt-5" style="display: block;">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">Edit Task</h5>
            <button type="button" class="btn-close" aria-label="Close" @click="closePopup"></button>
          </div>
          <div class="modal-body">
            <form @submit.prevent="submitEdit">
              <div class="mb-3">
                <label for="taskName" class="form-label">Name</label>
                <input type="text" class="form-control" id="taskName" v-model="editedTask.name">
              </div>
              <div class="mb-3">
                <label for="taskTime" class="form-label">Time</label>
                <input type="number" class="form-control" id="taskTime" v-model.number="editedTask.time">
              </div>
              <button type="submit" class="btn btn-success me-3 px-4">Submit</button>
              <button type="button" class="btn btn-secondary" @click="closePopup">Cancel</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const tasks = ref([
  { name: 'Task 1', time: 30 },
  { name: 'Task 2', time: 40 },
  { name: 'Task 3', time: 60 },
  { name: 'Task 4', time: 45 },
  { name: 'Task 5', time: 50 },
]);

const showPopup = ref(false);
const selectedIndex = ref(null);
const editedTask = ref({ name: '', time: 0 });

const editTask = (index) => {
  selectedIndex.value = index;
  editedTask.value = { ...tasks.value[index] };
  showPopup.value = true;
};

const closePopup = () => {
  showPopup.value = false;
};

const submitEdit = () => {
  tasks.value[selectedIndex.value] = editedTask.value;
  showPopup.value = false;
};
</script>
