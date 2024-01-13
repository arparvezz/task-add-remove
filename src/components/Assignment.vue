<script setup>
import { ref } from 'vue';

let tasks = ref([
  {
    name: 'Task 1',
    time: 60
  }, {
    name: 'Task 2',
    time: 36
  }
])

// Remove task item when delete button clicked
function removeItem(index) {
  tasks.value.splice(index, 1)
}

// show Modal for enter new Task 
let showPopup = ref(false)

// Add new Task 
function addNewTask() {
  let itemName = document.querySelector('#task-name').value;
  let itemTime = document.querySelector('#time').value;


  // Check either those fields are empty or not
  if (itemName == '' || itemTime == '') {
    alert("Field empty!")
    showPopup.value = true;
  } else {
    let item = {
      name: itemName,
      time: itemTime
    }
    tasks.value.push(item)
    clearValue()
  }
}

// clear the popup's input value
function clearValue() {
  document.querySelector('#task-name').value = ''
  document.querySelector('#time').value = ''
}




</script>
<template>
  <div class="container mx-auto my-4 p-4">

    <h2 class="text-xl text-center">Task Add/Delete</h2>
    <!-- task loop -->
    <div class="my-2 flex justify-between items-center bg-slate-100 p-3 rounded" v-for="(task, index) in tasks"
      :key="index">
      <p><strong>{{ index + 1 }}.</strong>  {{ task.name }}: <span>Time - {{ task.time }}</span></p>
      <button @click="removeItem(index)"
        class="bg-red-100 text-red-500 px-2 py-1 rounded hover:bg-red-200">Delete</button>
    </div>

   
 <!-- Add Task Button -->
 <button @click="showPopup = !showPopup" class="my-4 bg-blue-200 text-blue-600 px-4 py-2 rounded hover:bg-blue-300">Add New
      Task</button>
      

    <div class="bg-slate-200 p-5" v-show="showPopup">
      <label for="task-name">Enter Task Name</label><br>
      <input class="w-full p-2 border border-slate-200 rounded" type="text" name="task-name" id="task-name"
        placeholder="Task 99"><br>
      <label class="mt-3" for="time">Enter Time</label><br>
      <input class="w-full p-2 border border-slate-200 rounded" type="number" name="time" id="time" placeholder="42"><br>
      <button @click.prevent="addNewTask(); showPopup = false"
        class="my-4 bg-green-200 text-green-600 px-4 py-2 rounded hover:bg-green-300">Add
        Now</button>
      <button @click="showPopup = false"
        class="my-4 ml-2 bg-red-200 text-red-600 px-4 py-2 rounded hover:bg-red-300">Cancel</button>
    </div>

  </div>
</template>
<style></style>
