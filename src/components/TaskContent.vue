<template>
  <div class="main-container">
    <div class="flex justify-center mt-4">
      <div class="inline-flex rounded-lg overflow-hidden shadow">
        <button
          class="px-4 py-2 bg-gray-800 text-white hover:bg-gray-700 focus:outline-none active:bg-blue-600"
        >
          All
        </button>
        <button
          class="px-4 py-2 border-l border-gray-600 bg-gray-800 text-white hover:bg-gray-700 focus:outline-none active:bg-blue-600"
        >
          Pending
        </button>
        <button
          class="px-4 py-2 border-l border-gray-600 bg-gray-800 text-white hover:bg-gray-700 focus:outline-none active:bg-blue-600"
        >
          Completed
        </button>
      </div>
    </div>

    <!-- task and btn -->
    <div class="flex justify-between mt-8 px-8">
      <h2 class="text-4xl font-bold">Task lists</h2>

      <div class="flex">
        <input
          type="text"
          v-model="newTaskTitle"
          class="mx-2 px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
          placeholder="Enter text here"
        />

        <select
          v-model="newTaskCategory"
          class="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 mx-2"
        >
          <option v-for="(category, index) in categories" :key="index" :value="category">
            {{ category }}
          </option>
        </select>

        <div
          @click="addTask"
          class="px-4 py-2 border-l border-gray-600 bg-gray-800 text-white hover:bg-gray-700 focus:outline-none active:bg-blue-600 rounded-lg cursor-pointer"
        >
          <i class="ri-add-line text-white-500 text-2xl mx-2"></i>
          <button>Add Task</button>
        </div>
      </div>
    </div>

    <!-- task list -->
    <div class="w-full p-8">
      <table class="table-auto w-full border-collapse table-fixed">
        <thead class="bg-blue-900">
          <tr>
            <th class="px-4 py-2 text-left border w-1/10">SN</th>
            <th class="px-4 py-2 text-left border w-1/4">Task Name</th>
            <th class="px-4 py-2 text-left border w-1/4">Categories</th>
            <th class="px-4 py-2 text-left border w-1/4">Status</th>
            <th class="px-4 py-2 text-left border w-1/4">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td class="px-4 py-2 border">{{ index + 1 }}</td>
            <td class="px-4 py-2 border">{{ task.tasktitle }}</td>
            <td class="px-4 py-2 border">{{ task.category }}</td>
            <td class="px-4 py-2 border">{{ task.status }}</td>
            <td class="px-4 py-2 border flex">
              <div
                @click="toggleStatus(task)"
                class="px-4 py-2 border-l border-gray-600 bg-gray-800 text-white hover:bg-gray-700 focus:outline-none active:bg-blue-600 rounded-lg cursor-pointer"
              >
                <i class="ri-check-line text-white-500 text-2xl mx-2"></i>
                <button>{{ task.status === 'pending' ? 'Complete' : 'Revert' }}</button>
              </div>

              <div
                @click="deleteTask(index)"
                class="mx-2 px-4 py-2 border-l border-red-600 bg-red-800 text-white hover:bg-gray-700 focus:outline-none active:bg-red-600 rounded-lg cursor-pointer"
              >
                <i class="ri-delete-bin-6-line text-white-500 text-2xl mx-2"></i>
                <button>Delete</button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const tasks = ref([
  { tasktitle: 'reading', category: 'Learning', status: 'pending' },
  { tasktitle: 'Shopping for groceries', category: 'Shopping', status: 'Completed' },
])

const categories = ['Personal', 'Shopping', 'Learning and Education']

const newTaskTitle = ref('')
const newTaskCategory = ref('Personal')

function addTask() {
  if (newTaskTitle.value.trim()) {
    tasks.value.push({
      tasktitle: newTaskTitle.value,
      category: newTaskCategory.value,
      status: 'pending',
    })
    newTaskTitle.value = ''
    newTaskCategory.value = 'Personal'
  }
}

function toggleStatus(task) {
  task.status = task.status === 'pending' ? 'Completed' : 'pending'
}

function deleteTask(index) {
  tasks.value.splice(index, 1)
}
</script>

<style scoped></style>
