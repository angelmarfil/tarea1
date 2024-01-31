<script setup lang="ts">
import type { Ref } from 'vue'
import { ref, nextTick } from 'vue'

const name: Ref<string> = ref('')
const lastName: Ref<string> = ref('')
const age: Ref<string> = ref('')
const gender: Ref<string> = ref('masculino')
const otherGender: Ref<string> = ref('')
const isFormValid = ref(true)

const errors: Ref<Record<string, string>> = ref({})

const validation = (field: string) => {
  errors.value = { ...errors.value, [field]: '' }

  switch (field) {
    case 'name':
      if (name.value.length < 5 || name.value.length > 18) {
        errors.value[field] = 'Error de longitud en el nombre (mínimo 5, máximo 18 caracteres).'
      }
      break

    case 'lastName':
      if (lastName.value === name.value) {
        errors.value[field] = 'El apellido no puede ser igual al nombre.'
      }
      break

    case 'age':
      if (age.value !== '' && (age.value <= '0' || age.value >= '60')) {
        errors.value[field] = 'Error en la edad (debe ser mayor a 0 y menor a 60).'
      }
      break

    case 'gender':
      if (gender.value === 'otro' && (!otherGender.value || otherGender.value.trim() === '')) {
        errors.value['gender'] = "Especificar género si selecciona 'Otro'."
      } else {
        errors.value['otherGender'] = ''
      }
      break

    case 'otherGender':
      if (gender.value === 'otro' && (!otherGender.value || otherGender.value.trim() === '')) {
        errors.value[field] = 'Debe especificar el género.'
      } else {
        errors.value['gender'] = ''
      }
      break

    default:
      break
  }
  validateForm()
}

const validateForm = () => {
  nextTick(() => {
    isFormValid.value = Object.values(errors.value).every((error) => error === '')
  })
}

const handleSubmit = () => {
  if (isFormValid.value) {
    console.log('Formulario válido. Enviar datos...')
  }
}
</script>

<template>
  <main>
    <h1>Validación de Formulario</h1>
    <form @submit.prevent="handleSubmit">
      <div>
        <label for="name">Nombre:</label>
        <input @input="validation('name')" v-model="name" type="text" id="name" required />
        <span v-if="errors.name" class="error">{{ errors.name }}</span>
      </div>

      <div>
        <label for="lastName">Apellido:</label>
        <input
          @input="validation('lastName')"
          v-model="lastName"
          type="text"
          id="lastName"
          required
        />
        <span v-if="errors.lastName" class="error">{{ errors.lastName }}</span>
      </div>

      <div>
        <label for="age">Edad:</label>
        <input @input="validation('age')" v-model="age" type="number" id="age" required />
        <span v-if="errors.age" class="error">{{ errors.age }}</span>
      </div>

      <div>
        <label for="gender">Género:</label>
        <select v-model="gender" @change="validation('gender')" id="gender">
          <option value="masculino">Masculino</option>
          <option value="femenino">Femenino</option>
          <option value="otro">Otro</option>
        </select>
        <input
          v-if="gender === 'otro'"
          @input="validation('otherGender')"
          v-model="otherGender"
          type="text"
          placeholder="Especificar género"
        />
        <span v-if="errors.gender" class="error">{{ errors.gender }}</span>
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
