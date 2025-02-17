<script setup>
  import image from '../assets/img/grafico.jpg';
import { formatBudget } from '../helpers';

  const props = defineProps({
    budget: {
      type: Number, 
      required: true
    },
    available: {
      type: Number, 
      required: true
    }
  })

</script>

<template>
  <div class="two-cols">
    <div class="graphic-container">
      <img
        :src="image"
      />
    </div>

    <div class="budget-container">
      <button 
        class="reset-app"
      >
        Reset App
      </button>

      <p>
        <span>Budget:</span>
        {{ formatBudget(budget) }}
      </p>
      
      <p>
        <span>Available:</span>
        {{ formatBudget(available) }}
      </p>

      <p>
        <span>Spent:</span>
        $0
      </p>
    </div>
  </div>
</template>


<style scoped>
  .two-cols {
    display: flex;
    flex-direction: column;
  }

  .two-cols > :first-child {
    margin-bottom: 3rem;
  }

  @media (min-width: 768px) {

    .two-cols {
      flex-direction: row;
      gap: 4rem;
      align-items: center;
    }

    .two-cols > :first-child {
      margin-bottom: 0rem;
    }
  }

  .reset-app {
    background-color: #DB2777;
    border: none;
    padding: 1rem;
    width: 100%;
    color: var(--blanco);
    font-weight: 900;
    text-transform: uppercase;
    border-radius: 1rem;
    transition-property: background-color;
    transition-duration: 300ms;
  }

  .reset-app:hover {
    cursor: pointer;
    background-color: #b7155e;

  }

  .budget-container {
      width: 100%;
    }

  .budget-container p {
    font-size: 2.4rem;
    text-align: center;
    color: var(--gris-oscuro);
  }

  @media (min-width: 768px) {
  .budget-container p {
    text-align: left;
  }
  }

  .budget-container span {
    font-weight: 900;
    color: var(--azul);
  }
</style>