<template>
  <div class="form-container">
    <h2 class="form-heading">Indtast din artikel</h2>
    <form @submit.prevent="submitForm" class="form">
      <div class="form-group">
        <label for="header" class="form-label">Overskrift:</label>
        <input type="text" id="header" class="form-input" v-model="header" />
        <p v-if="headerError" class="error-message">{{ headerError }}</p>
      </div>
      <div class="form-group">
        <label for="info" class="form-label">Tekst:</label>
        <textarea id="info" class="form-textarea" v-model="info"></textarea>
        <p v-if="infoError" class="error-message">{{ infoError }}</p>
      </div>
      <button type="submit" class="submit-button">Tilføj til vidensbanken</button>
    </form>
  </div>
</template>

<script setup>
import { supabase } from '../lib/supabaseClient.js'
import { ref } from 'vue'

const header = ref('')
const info = ref('')
const headerError = ref(null)
const infoError = ref(null)

const submitForm = async () => {
  if (validateForm()) {
    const { data, error } = await supabase.from('vidensinfo').upsert([
      {
        header: header.value,
        info: info.value
      }
    ])

    if (error) {
      console.error('An error occurred while submitting the form:', error)
    } else {
      header.value = '';
      info.value = '';
      alert('Du har nu tilføjet noget til din vidensbank - Hvor er du god mus ❤️❤️❤️') 
      console.log('Form submitted successfully:', data)
    }
  }
}

const validateForm = () => {
  if (!header.value || header.value.length < 4) {
    headerError.value = 'Overskrift skal være mindst 4 tegn.';
    return false;
  }

  if (!info.value || info.value.length < 1) {
    infoError.value = 'Hov der skal være noget Tekst';
    return false;
  }


  headerError.value = null;
  infoError.value = null;
  return true;
}
</script>

<style scoped>
.form-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px;
  background-color: #fff; /* White background */
  border-radius: 8px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 400px;
  margin: 20px auto; /* Center the form horizontally */
  box-sizing: border-box; /* Ensure padding doesn't affect width */
}

.form-heading {
  text-align: center;
  font-size: 1.5rem;
  margin-bottom: 20px;
  color: #ff6666; /* Rose color */
}

.form-group {
  margin-bottom: 15px;
}

.form-label {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
  color: grey;
}

.form-input,
.form-textarea {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  transition: border-color 0.2s;
}

.form-input:focus,
.form-textarea:focus {
  outline: none;
  border-color: #ff6666; /* Highlight border color on focus */
}

.submit-button {
  display: block;
  width: 100%;
  padding: 10px;
  background-color: #ff6666; /* Rose button color */
  border: none;
  border-radius: 4px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.2s;
}

.submit-button:hover {
  background-color: #ff3333; /* Darker rose button color on hover */
}

.error-message {
  color: red;
  margin-top: 5px;
  font-size: 0.875rem; /* Adjust the font size as needed */
}
</style>
