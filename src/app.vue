<script setup>
import DeveloperRegistration from "./presentation/components/developer-registration.vue";
import {ref} from "vue"; //Actualiza automaticamente cuando cambia.
import {Developer} from "./greetings/domain/model/developer.entity.js";
import DeveloperCountShow from "./presentation/components/developer-count-show.vue";
import DeveloperGreeting from "./presentation/components/developer-greeting.vue";

//Creando 3 variables que empiezan vacias.
const firstName = ref('');
const lastName = ref('');
const developerCount = ref(0);
const hasRegistered = ref(false);

function updateRegisteredDeveloperInfo(developer){
  firstName.value = developer.firstName;
  lastName.value = developer.lastName;
  hasRegistered.value = true;
  console.log('Developer registered:', developer);
  updateDeveloperCount(developer);
}

function resetRegisteredDeveloperInfo(){
  firstName.value = '';
  lastName.value = '';
  hasRegistered.value = false;
  console.log('Registration deferred');
}

function updateDeveloperCount(developer){
  const dev = new Developer(developer.firstName, developer.lastName);
  if (dev.firstName !== 'Unknown')
    developerCount.value++;
}
</script>

<template>
  <h1>Hello Vue Developer Application</h1>
  <developer-registration
    @developer-registered="updateRegisteredDeveloperInfo"
    @registration-deferred="resetRegisteredDeveloperInfo"/>
  <developer-greeting v-if="hasRegistered" :first-name="firstName" :last-name="lastName"/>
  <developer-count-show :developer-count="developerCount"/>
</template>
