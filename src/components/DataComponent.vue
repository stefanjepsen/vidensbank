<template>
  <div class="data-container">
    <h2 class="data-heading">Supabase Data Component</h2>
    <div class="search-container">
      <input type="text" v-model="searchQuery" placeholder="Search...">
    </div>
    <div v-if="loading" class="loading">Loading data...</div>
    <div v-else class="data-content">
      <div v-for="(item, index) in filteredData" :key="index" :class="{ 'data-card': true, 'zoom-card': item.isEditing }">
        <div v-if="!item.isEditing">
          <div class="data-card-header">{{ item.header }}</div>
          <div class="divider"></div>
          <div class="data-card-info">{{ item.info }}</div>
          <button @click="showConfirmation(index)" class="delete-button">Delete</button>
          <button @click="toggleEdit(index)" class="edit-button">Edit</button>
        </div>
        <div v-else>
          <input v-model="item.header" class="edit-header" />
          <textarea v-model="item.info" class="edit-info"></textarea>
          <button @click="saveEdit(index)" class="save-button">Save</button>
        </div>
      </div>
    </div>

    <!-- Delete Confirmation Popup -->
    <div v-if="showPopup" class="popup">
      <div class="popup-content">
        <p>Er du sikker på du vil slette denne? ?</p>
        <button @click="deleteItem">Yes</button>
        <button @click="cancelDelete">No</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'
import { supabase } from '../lib/supabaseClient' // Import your supabase instance here

const data = ref([])
const loading = ref(true)
const selectedIndex = ref(null)
const showPopup = ref(false)
const searchQuery = ref('')

onMounted(async () => {
  try {
    const { data: fetchData, error } = await supabase.from('vidensinfo').select('*')
    if (error) {
      console.error('An error occurred while fetching data:', error)
    } else {
      data.value = fetchData.map((item) => ({
        ...item,
        isEditing: false, // Step 1: Add an 'isEditing' property
      }))
      loading.value = false
    }
  } catch (error) {
    console.error('An error occurred while fetching data:', error)
  }
})

const showConfirmation = (index) => {
  selectedIndex.value = index
  showPopup.value = true
}

const deleteItem = async () => {
  try {
    const itemToDelete = data.value[selectedIndex.value]
    const { error } = await supabase
      .from('vidensinfo')
      .delete()
      .eq('id', itemToDelete.id)

    if (error) {
      console.error('An error occurred while deleting data:', error)
    } else {
      data.value.splice(selectedIndex.value, 1)
      selectedIndex.value = null
      showPopup.value = false
    }
  } catch (error) {
    console.error('An error occurred while deleting data:', error)
  }
}

const cancelDelete = () => {
  selectedIndex.value = null
  showPopup.value = false
}

const toggleEdit = (index) => {
  data.value[index].isEditing = !data.value[index].isEditing
}

const saveEdit = async (index) => {
  const editedItem = data.value[index]
  try {
    const { error } = await supabase
      .from('vidensinfo')
      .upsert([{
        id: editedItem.id,
        header: editedItem.header,
        info: editedItem.info,
      }], { onConflict: ['id'] }) // Assuming 'id' is the primary key column

    if (error) {
      console.error('An error occurred while saving data:', error)
    } else {
      editedItem.isEditing = false
    }
  } catch (error) {
    console.error('An error occurred while saving data:', error)
  }
}

const filteredData = computed(() => {
  return data.value.filter((item) => {
    const searchTerm = searchQuery.value.toLowerCase()
    return item.header.toLowerCase().includes(searchTerm) || item.info.toLowerCase().includes(searchTerm)
  })
})
</script>

<style scoped>
.data-container {
  text-align: center;
  padding: 20px;
}

.data-heading {
  font-size: 1.5rem;
  margin-bottom: 20px;
}

.loading {
  font-style: italic;
  color: #666;
}

.search-container {
  margin-bottom: 20px;
}

.search-container input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.data-content {
  display: flex;
  flex-wrap: wrap;
}

.data-card {
  background-color: white;
  border-radius: 8px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin: 10px;
  width: 300px;
  transition: transform 0.3s ease-in-out; /* Add a smooth transition effect */
}

.data-card-header {
  font-weight: bold;
  margin-bottom: 20px;
  color: #000;
}

.data-card-info {
  color: #333;
  text-align: left;
}

.delete-button {
  margin-top: 10px;
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 6px 12px;
  cursor: pointer;
}

.edit-button {
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 6px 12px;
  margin-right: 5px;
  cursor: pointer;
}

.save-button {
  background-color: #008CBA;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 6px 12px;
  margin-right: 5px;
  cursor: pointer;
}

.popup {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.popup-content {
  background-color: white;
  padding: 20px;
  border-radius: 4px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
  text-align: center;
  color: #333;
}

.divider {
  border-bottom: 1px #3333338c solid;
  width: 100%;
}

/* Additional styles for editing mode */
.edit-header,
.edit-info {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

/* CSS for the zoom effect */
.zoom-card {
  transform: scale(1.2); /* Increase the scale to zoom in */
  transition: transform 0.3s ease-in-out; /* Add a smooth transition effect */
  z-index: 2; /* Bring the card to the front */
  position: absolute; /* Position the card in the center */
  top: 50%;
/*  left: 50%; */
  transform-origin: center center;
}
</style>
