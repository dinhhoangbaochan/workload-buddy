<template>
  <div class="pixel-container">
    <h1 class="pixel-heading">Workload Buddy</h1>
    <div class="pixel-form">
      <p>Add your task via the input below.</p>
      <input type="text" v-model="message" class="pixel-input" placeholder="Name your task">
      <button v-on:click="submit" class="pixel-button">Add Task</button>
      <button v-if="editingIndex !== null" v-on:click="cancelEdit" class="pixel-button">Cancel Edit</button>

      <div v-for="(item, index) in list" :key="index" class="pixel-item">
        - {{ item }} 
        <a v-on:click="modify(item, index)" class="pixel-link">Edit</a> | 
        <a v-on:click="remove(index)" class="pixel-link">Delete</a>
      </div>
    </div>
  </div>
</template>

<script setup>

const message = ref('');
const list = ref([]);
const editingIndex = ref(null);

const submit = () => {
  // Check if the input is not empty
  if (message.value.trim() !== '') {
    if (editingIndex.value !== null) {
      // Update the existing item
      list.value[editingIndex.value] = message.value;
      editingIndex.value = null;
    } else {
      // Add a new item
      list.value.push(message.value);
    }
  } else {
    // Optional: Alert the user if they try to submit an empty input
    alert('Please enter a value!');
  }
  message.value = '';
}

const modify = (val, index) => {
  message.value = val;
  editingIndex.value = index;
}

const remove = (index) => {
  list.value.splice(index, 1);
  if (editingIndex.value === index) {
    editingIndex.value = null;
    message.value = '';
  }
}

const cancelEdit = () => {
  editingIndex.value = null;
  message.value = '';
}
</script>

<style>
.pixel-container {
  text-align: center; /* Centering the heading and form */
}

.pixel-heading {
  font-family: 'Press Start 2P', cursive;
  color: #ff66b2; /* Bright pink color for the heading */
  text-shadow: 1px 1px #ff99c8; /* Slight shadow for a 3D effect */
  margin-bottom: 20px; /* Spacing between heading and form */
}

.pixel-form {
  background-color: #ffccf9; /* Light pink background */
  padding: 20px;
  border: 3px solid #ff66b2; /* Darker pink border */
  width: 50%; /* Smaller width */
  margin: 0 auto; /* Centering the form */
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2); /* Adding a subtle shadow */
  font-family: 'Press Start 2P', cursive;
}

.pixel-input, .pixel-button {
  font-family: 'Press Start 2P', cursive;
  background-color: #ffe6f2; /* Very light pink */
  border: 2px solid #ff99c8; /* Medium pink */
  padding: 5px;
  margin: 5px 0;
 /* Adjusting width for better layout */
}

.pixel-input {
  width: 98%
}

.pixel-button {
  cursor: pointer;
  background-color: #ff66b2; /* Bright pink */
  color: white;
  display: block; /* Make buttons block level for full width */
  margin: 10px 0; /* Add margin for spacing */
  width: 100%;
}

.pixel-item {
  margin: 10px 0;
  color: #663399; /* Contrasting color for text */
}

.pixel-link {
  color: #ff3399; /* Pink color for links */
  text-decoration: none;
  cursor: pointer;
  font-size: 0.8em;
}

.pixel-link:hover {
  text-decoration: underline;
}
</style>