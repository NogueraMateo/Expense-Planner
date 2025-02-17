<script setup>
  import { ref } from 'vue';
  import Alert from './Alert.vue';
  import closeModal from '../assets/img/cerrar.svg';

  const error = ref('')

  const emit = defineEmits(['close-modal', 'save-expense', 'update:name', 'update:amount', 'update:category'])
  const props = defineProps({
    modal: {
      type: Object,
      required: true
    },
    name : {
      type: String, 
      required: true
    },
    amount: {
      type: [String, Number],
      required: true
    },
    category: {
      type: String,
      required: true
    }
  })

  const validateBudget = () => {
    // Validate there are not empty fields
    const { name, amount, category } = props

    if ([name, amount, category].includes('')) {
      error.value = 'All fields are required'

      setTimeout(() => {
        error.value = ''
      }, 3000);

      return
    }

    if (amount <= 0) {
      error.value = 'Invalid amount'

      setTimeout(() => {
        error.value = ''
      }, 3000);
       
      return  
    }

    emit('save-expense')
  }

</script>

<template>
  <div class="modal">
    <div 
      class="close-modal"
      @click="$emit('close-modal')"
    >
      <img 
        :src="closeModal"
        alt="Close modal"
      />
    </div>

    <div 
      class="container form-container"
      :class="[modal.animate ? 'animate' : 'close']"
    >
      <form
        class="new-expense"
        @submit.prevent="validateBudget"
      >
        <legend>Add expense</legend>
        
        <Alert v-if="error">
          {{ error }}
        </Alert>

        <div class="field">
          <label for="name">Expense name:</label>
          <input
            type="text"
            id="name"
            placeholder="Add the expense name"
            :value="name"
            @input="$emit('update:name', $event.target.value)"
          />
        </div>

        <div class="field">
          <label for="amount">Amount:</label>
          <input
            type="text"
            id="amount"
            placeholder="Add the amount of the expense. E.g. 300"
            @input="$emit('update:amount', $event.target.value)"
            :value="amount"
          />
        </div>

        <div class="field">
          <label for="category">Category:</label>
          <select 
            name="category" 
            id="category"
            @input="$emit('update:category', $event.target.value)"
            :value="category"
            >
            <option value="">-- Select --</option>
            <option value="savings">Savings</option>
            <option value="food">Food</option>
            <option value="house">House</option>
            <option value="expenses">Expenses</option>
            <option value="leisure">Leisure</option>
            <option value="health">Health</option>
            <option value="memberships">Memberships</option>
          </select>
        </div>

        <input 
          type="submit"
          value="Add expense"
          
        />
      </form>
    </div>
  </div>
</template>

<style scoped>
  .modal {
    position: absolute;
    background-color: rgb(0 0 0 / 0.9);
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
}

  .close-modal {
    position: absolute;
    right: 3rem;
    top: 3rem;
  }

  .close-modal img {
    width: 3rem;
    cursor: pointer;
  }

  .form-container {
    transition-property: all;
    transition-duration: 300ms;
    transition-timing-function: ease-in;
    opacity: 0;
  }

  .form-container.animate {
    opacity: 1;
  }

  .form-container.close {
    opacity: 0;
  }

  .new-expense {
    margin: 10rem auto 0 auto;
    display: grid;
    gap: 2rem;
  }

  .new-expense legend {
    text-align: center;
    color: var(--blanco);
    font-size: 3rem;
    font-weight: 700;
  }

  .field {
    display: grid;
    gap: 2rem;
  }

  .new-expense input,
  .new-expense select {
    background-color: var(--gris-claro);
    border-radius: 1rem;
    padding: 1rem;
    border: none;
    font-size: 2.2rem;
  }

  .new-expense label {
    color: var(--blanco);
    font-size: 3rem;
  }

  .new-expense input[type="submit"] {
    background-color: var(--azul);
    color: var(--blanco);
    font-weight: 700;
    cursor: pointer;
  }
</style>