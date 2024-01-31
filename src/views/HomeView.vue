<template>
  <main class="form-container">
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
      <div class="gender-input">
        <select v-model="gender" @change="handleInput('gender')" id="gender">
          <option value="masculino">Masculino</option>
          <option value="femenino">Femenino</option>
          <option value="otro">Otro</option>
        </select>
        <input v-if="gender === 'otro'" @input="handleInput('otherGender')" v-model="otherGender" type="text" placeholder="Especificar género">
      </div>
    </div>

    <h1 :style="{ color: isValid('name') ? 'green' : 'red' }">{{ name }}</h1>
    <h2 :class="{ 'error': !isValid('age') && age !== '' }">{{ age }}</h2>

    <h3 v-if="errors.length > 0">Errores:</h3>
    <span v-for="errorMessage in errors" :key="errorMessage" class="error-message">{{ errorMessage }}</span>
  </main>
</template>

<style scoped>
  .form-container {
    max-width: 400px;
    margin: 0 auto;
  }

  .form-group {
    margin-bottom: 1.5em;
  }

  label {
    display: block;
    margin-bottom: 0.5em;
    font-weight: bold;
  }

  input, select {
    width: 100%;
    padding: 0.5em;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
  }

  .gender-input {
    display: flex;
    gap: 0.5em;
  }

  .error {
    color: red;
  }

  .error-message {
    color: red;
    margin-bottom: 1rem;
    display: block;
  }
</style>
