<template>
  <main>
    <div class="form-group">
      <label for="name">Nombre:</label>
      <input @input="handleInput('name')" v-model="name" type="text" id="name">
    </div>

    <div class="form-group">
      <label for="lastName">Apellido:</label>
      <input @input="handleInput('lastName')" v-model="lastName" type="text" id="lastName">
    </div>

    <div class="form-group">
      <label for="age">Edad:</label>
      <input @input="handleInput('age')" v-model="age" type="number" id="age">
    </div>

    <div class="form-group">
      <label for="gender">Género:</label>
      <select v-model="gender" @change="handleInput('gender')" id="gender">
        <option value="masculino">Masculino</option>
        <option value="femenino">Femenino</option>
        <option value="otro">Otro</option>
      </select>
      <input v-if="gender === 'otro'" @input="handleInput('otherGender')" v-model="otherGender" type="text" placeholder="Especificar género">
    </div>

    <h1 :style="{ color: isValid('name') ? 'green' : 'red' }">{{ name }}</h1>
    <h2 :class="{ 'error': !isValid('age') && age !== '' }">{{ age }}</h2>

    <h3 v-if="errors.length > 0">Errores:</h3>
    <span v-for="errorMessage in errors" :key="errorMessage" :style="{ color: 'red', marginBottom: '1rem', display: 'block' }">{{ errorMessage }}</span>
  </main>
</template>

<script setup lang="ts">
import { ref } from "vue";
import type { Ref } from "vue";

const name: Ref<string> = ref("Marfil");
const lastName: Ref<string> = ref("");
const age: Ref<number | string> = ref(""); 
const gender: Ref<string> = ref("masculino");
const otherGender: Ref<string> = ref("");

const errors: Ref<string[]> = ref([]);

const handleInput = (field: string) => {
  validation(field);
};

const validation = (field: string) => {
  errors.value = [];

  switch (field) {
    case 'name':
      if (name.value.length < 5 || name.value.length > 18) {
        errors.value.push("Error de longitud en el nombre (mínimo 5, máximo 18 caracteres).");
      }
      break;

    case 'lastName':
      if (lastName.value === name.value) {
        errors.value.push("El apellido no puede ser igual al nombre.");
      }
      break;

    case 'age':
      if (age.value !== '' && (age.value <= 0 || age.value >= 60)) {
        errors.value.push("Error en la edad (debe ser mayor a 0 y menor a 60).");
      }
      break;

    case 'gender':
      if (gender.value === "otro" && !otherGender.value) {
        errors.value.push("Especificar género si selecciona 'Otro'.");
      }
      break;

    case 'otherGender':
      // Validaciones específicas para otherGender, si es necesario
      break;

    default:
      break;
  }
};

const isValid = (field: string) => {
  switch (field) {
    case 'name':
      return name.value.length >= 5 && name.value.length <= 18;
    case 'age':
      return age.value === '' || (age.value > 0 && age.value < 60);
    default:
      return true;
  }
};
</script>

<style scoped>
  .form-group {
    margin-bottom: 1em;
  }

  .error {
    color: red;
  }
</style>

