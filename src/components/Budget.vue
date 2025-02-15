<script setup>
  import { ref } from 'vue';
  import Alert from './Alert.vue';

  const budget = ref(0)
  const error = ref('')

  const setBudget = () => {
    if (budget.value <= 0) {
      error.value = 'Invalid Budget'
      
      setTimeout(() => {
        error.value = ''
      }, 3000)
    }
  }
</script>

<template>
  <form 
    action=""
    class="budget"
    @submit.prevent="setBudget"
  >

    <Alert v-if="error">
      {{ error }}
    </Alert>

    <div class="field">
      <label 
        for="define-budget"
      >
        Set Budget
      </label>

      <input 
        type="number"
        class="define-budget"
        id="define-budget"
        placeholder="Add your budget"
        min="0"
        v-model.number="budget"
      />
    </div>

    <input 
      type="submit"
      value="Set Budget"
    />
  </form>
</template>

<style scoped>

  .budget {
    width: 100%;
  }

  .field {
    display: grid;
    gap: 2rem;
  }

  .budget label {
    font-size: 2.2rem;
    text-align: center;
    color: var(--azul);
  }


  .budget input[type="number"] {
    background-color: var(--gris-claro);
    border-radius: 1rem;
    padding: 1rem;
    border: none;
    font-size: 2.2rem;
    text-align: center;
  }

  .budget input[type="submit"]  {
    background-color: var(--azul);
    border: none;
    padding: 1rem;
    text-align: center;
    font-size: 2rem;
    margin-top: 2rem;
    color: var(--blanco);
    font-weight: 900;
    width: 100%;
    transition: background-color 300ms ease;
  }

  .budget input[type="submit"]:hover {
    background-color: #1048A4;
    cursor: pointer;
  }


</style>