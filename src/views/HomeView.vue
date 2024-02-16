<script setup lang="ts">
import type { ComputedRef, Ref } from 'vue'
import { ref, computed } from 'vue'

const name: Ref<string> = ref('')

const nameValidation = computed(() =>
  (name.value.length > 0 && name.value.length < 5) || name.value.length > 18
    ? 'Error de longitud en el nombre (mínimo 5, máximo 18 caracteres)'
    : ''
)

const lastName: Ref<string> = ref('')

const lastNameValidation = computed(() =>
  lastName.value.length > 0 && lastName.value === name.value
    ? 'El apellido no puede ser igual al nombre'
    : ''
)

const age: Ref<string> = ref('')

const ageValidation = computed(() =>
  (age.value !== '' && age.value <= '0') || age.value >= '60'
    ? 'Error en la edad (debe ser mayor a 0 y menor a 60)'
    : ''
)

const gender: Ref<string> = ref('masculino')

const genderValidation = computed(() =>
  gender.value === 'otro' && !otherGender.value ? 'Debe especificar el género.' : ''
)

const otherGender: Ref<string> = ref('')

const isFormValid: ComputedRef<boolean> = computed(
  () =>
    !(
      nameValidation.value.length > 0 ||
      lastNameValidation.value.length > 0 ||
      ageValidation.value.length > 0 ||
      genderValidation.value.length > 0
    )
)

const handleSubmit = () => {
  if (isFormValid.value) {
    console.log('Formulario válido. Enviar datos...')
    alert('Formulario válido.')
  }
}
</script>

<template>
  <main>
    <h1>Validación de Formulario</h1>
    <form @submit.prevent="handleSubmit">
      <div>
        <label for="name">Nombre:</label>
        <input v-model.trim="name" type="text" id="name" required />
        <span v-if="nameValidation" class="error">{{ nameValidation }}</span>
      </div>

      <div>
        <label for="lastName">Apellido:</label>
        <input v-model.trim="lastName" type="text" id="lastName" required />
        <span v-if="lastNameValidation" class="error">{{ lastNameValidation }}</span>
      </div>

      <div>
        <label for="age">Edad:</label>
        <input v-model="age" type="number" id="age" required />
        <span v-if="ageValidation" class="error">{{ ageValidation }}</span>
      </div>

      <div>
        <label for="gender">Género:</label>
        <select v-model="gender" id="gender">
          <option value="masculino">Masculino</option>
          <option value="femenino">Femenino</option>
          <option value="otro">Otro</option>
        </select>
        <input
          v-if="gender === 'otro'"
          v-model.trim="otherGender"
          type="text"
          placeholder="Especificar género"
        />
        <span v-if="genderValidation" class="error">{{ genderValidation }}</span>
      </div>

      <button :disabled="!isFormValid" type="submit">Enviar!</button>
    </form>
  </main>
</template>

<style scoped>
h1 {
  text-transform: uppercase;
  font-family: 'Bakbak One';
  color: var(--secondary-color);
  margin-top: 2rem;
}

main {
  display: grid;
  place-items: center;
  height: 100vh;
}

form {
  box-shadow:
    rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
  margin-top: 1rem;
  padding: 30px;
  display: flex;
  flex-direction: column;
  row-gap: 1rem;
  background-color: var(--white-color);

  & div {
    width: 300px;
    margin-bottom: 1em;
  }

  & label {
    display: block;
    margin-bottom: 0.5em;
  }

  & input {
    appearance: none;
    border: 1px solid #ccc;
    width: 100%;
    padding: 10px 20px;
    border-radius: 8px;
    font-size: 1rem;
  }

  & select {
    appearance: none;
    border: 1px solid #ccc;
    padding: 10px 20px;
    border-radius: 8px;
    font-size: 1rem;
  }

  & button {
    appearance: none;
    border: none;
    padding: 10px 20px;
    border-radius: 8px;
    font-size: 1rem;
    background-color: var(--primary-color);
    color: var(--white-color);
  }

  & button:disabled {
    cursor: not-allowed;
    background-color: #ccc;
    color: #666;
  }
}

.error {
  color: red;
  font-size: 0.8rem;
  display: block;
}
</style>
