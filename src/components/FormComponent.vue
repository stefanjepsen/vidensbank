<template>
  <div class="form-container">
    <h2 class="form-heading">Indtast vidensbank halløj</h2>
    <form @submit.prevent="submitForm" class="form">
      <div class="form-group">
        <label for="header" class="form-label">Overskrift:</label>
        <input type="text" id="header" class="form-input" v-model="header" />
      </div>
      <div class="form-group">
        <label for="info" class="form-label">Tekst:</label>
        <textarea id="info" class="form-textarea" v-model="info"></textarea>
      </div>
      <button type="submit" class="submit-button">OK</button>
    </form>
  </div>
</template>


<script setup>
import { supabase } from '../lib/supabaseClient.js'

import { ref } from 'vue'

const header = ref('')
const info = ref('')

const submitForm = async () => {
 // alert(header.value+ ' + ' + info.value)
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
</script>


<style scoped>
.form-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: auto;
  border: 1px solid #ffcccc; /* Rose background color */
}

.form {

  border-radius: 8px;
  padding: 20px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 400px;
  margin-top: 20px; /* Add some space between header and form */
}

.form-heading {
  text-align: center;
  font-size: 1.5rem;
  margin-bottom: 20px;
  color: #ffcccc;;
}

.form-group {
  margin-bottom: 15px;
}

.form-label {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
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
  border-color: #ff9999; /* Highlight border color on focus */
}

.submit-button {
  display: block;
  width: 100%;
  padding: 10px;
  background-color: #ff9999; /* Rose button color */
  border: none;
  border-radius: 4px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.2s;
}

.submit-button:hover {
  background-color: #ff6666; /* Darker rose button color on hover */
}
</style>