<!-- src/components/UserForm.vue -->
<template>
  <div class="container">
    <form @submit.prevent="submitForm">
    <div class="form-group">
      <label for="name">Nom :</label>
      <input type="text" id="name" v-model="name" @blur="validateName" />
      <span class="error-message" v-if="errors.name">{{ errors.name }}</span>
    </div>

    <div class="form-group">
      <label for="email">Email :</label>
      <input type="email" id="email" v-model="email" @blur="validateEmail" />
      <span class="error-message" v-if="errors.email">{{ errors.email }}</span>
    </div>

    <div class="form-group">
      <label for="phone">Numéro de téléphone :</label>
      <input type="tel" id="phone" v-model="phone" @blur="validatePhone" />
      <span class="error-message" v-if="errors.phone">{{ errors.phone }}</span>
    </div>

    <button type="submit">Soumettre</button>

    <div v-if="successMessage" class="success-message">
      {{ successMessage }}
    </div>
  </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Définir les variables réactives pour les champs du formulaire
const name = ref('');
const email = ref('');
const phone = ref('');

// Définir les erreurs
const errors = ref({
  name: '',
  email: '',
  phone: ''
});

// Message de succès
const successMessage = ref('');

// Valider le nom
const validateName = () => {
  if (!name.value) {
    errors.value.name = 'Le nom est requis.';
  } else if (name.value.length < 3) {
    errors.value.name = 'Le nom doit comporter au moins 3 caractères.';
  } else {
    errors.value.name = '';
  }
};

// Valider l'email
const validateEmail = () => {
  const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/;
  if (!email.value) {
    errors.value.email = 'L\'email est requis.';
  } else if (!emailPattern.test(email.value)) {
    errors.value.email = 'Veuillez entrer un email valide.';
  } else {
    errors.value.email = '';
  }
};

// Valider le numéro de téléphone
const validatePhone = () => {
  const phonePattern = /^\d{10}$/;
  if (!phone.value) {
    errors.value.phone = 'Le numéro de téléphone est requis.';
  } else if (!phonePattern.test(phone.value)) {
    errors.value.phone = 'Veuillez entrer un numéro de téléphone valide (10 chiffres).';
  } else {
    errors.value.phone = '';
  }
};

// Soumettre le formulaire
const submitForm = () => {
  validateName();
  validateEmail();
  validatePhone();

  if (!errors.value.name && !errors.value.email && !errors.value.phone) {
    successMessage.value = 'Formulaire soumis avec succès !';
  } else {
    successMessage.value = '';
  }
};
</script>

<style scoped>
.container{
  width: 100%;
  display: flex;
  justify-content: center;
  
}
form{
  width: 40%;

}
form label{
  display: flex;
}
.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

input[type="text"],
input[type="email"],
input[type="tel"] {
  width: 100%;
  padding: 8px;
  margin: 4px 0;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 10px 20px;
  background-color: #233cc7;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  width: 100%;
}

button:hover {
  background-color: #3c56e9;
}

.error-message {
  color: red;
  font-size: 0.9em;
}

.success-message {
  color: green;
  font-size: 1em;
  margin-top: 20px;
}
</style>
