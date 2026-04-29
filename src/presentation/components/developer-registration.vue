<script setup>
import {ref} from 'vue'; //Actualiza automaticamente cuando cambia.

//Creando 3 variables que empiezan vacias.
const firstName = ref('');
const lastName = ref('');
const errorMessage = ref('');
const emit = defineEmits(['developer-registered', 'registration-deferred']); //Envia eventos al componente padre.

function submitRegistrationRequest() { //Se ejecuta al enviar el formulario
  let submittedFirstName = firstName.value.toString().trim();
  let submittedLastName = lastName.value.toString().trim();
  if (submittedFirstName || submittedLastName) {
    console.log('Registering developer');
    emit('developer-registered', {
      firstName: submittedFirstName,
      lastName: submittedLastName
    });
    clearFields()
    errorMessage.value = '';
  } else {
    console.log('Cannot register: Both fields are required');
    errorMessage.value = 'Please provide at least a first name or a last name to register.' +
        'Warming: Both are required for a successful registration.';
  }
}

function deferRegistration() {
  console.log('Deferring registration');
  emit('registration-deferred', {firstName: '', lastName: ''});
  clearFields()
  errorMessage.value = '';
}

function clearFields() {
  firstName.value = '';
  lastName.value = '';
  errorMessage.value = '';
}
</script>

<template>
  <!-- Developer Registration Form -->
  <div>
    <h2>New Developer</h2>
    <div>
      <form v-on:submit.prevent="submitRegistrationRequest">
        <!-- Div for First Name -->
        <div class="field">
          <label for="first-name">First Name:</label>
          <input id="first-name" v-model="firstName" type="text"/>
        </div>
        <!-- Div for First Name -->
        <div class="field">
          <label for="last-name">Last Name:</label>
          <input id="last-name" v-model="lastName" type="text"/>
        </div>
        <!-- Action Buttons -->
        <div class="action">
          <button type="submit">Register</button>
          <button type="button" v-on:click="deferRegistration">Later</button>
          <button type="button" v-on:click="clearFields">Clear</button>
        </div>
      </form>
      <p v-if="errorMessage" class="error" role="alert">{{errorMessage}}</p>
    </div>
  </div>
</template>

<style scoped>
button {
  margin-top: 10px;
  padding: 8px 16px;
  cursor: pointer;
}

.error {
  color: red;
  margin-top: 10px;
  font-size: 14px;
}

.field {
  margin-bottom: 10px;
}

.action {
  margin-top: 10px;
}

label{
  margin-right: 5px;
}
</style>