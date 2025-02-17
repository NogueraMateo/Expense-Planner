<script setup>
  import { ref, reactive } from 'vue';
  import { uid } from 'uid';
  import Budget from './components/Budget.vue';
  import Modal from './components/Modal.vue';
  import Expense from './components/Expense.vue';
  import BudgetControl from './components/BudgetControl.vue';
  import newBudgetIcon from './assets/img/nuevo-gasto.svg'

  const modal = reactive({
    show: false,
    animate: false
  })
  const budget = ref(0);
  const available = ref(0);

  const expense = reactive({
    name: '',
    amount: '',
    category: '',
    id: null,
    date: Date.now()
  })

  const expenses = ref([]);

  const setBudget = (quantity) => {
    budget.value = quantity;
    available.value = quantity;
  }

  const showModal = () => {
    modal.show = true;
    setTimeout(() => {
      modal.animate = true;      
    }, 300);
  }
  
  const closeModal = () => {
    modal.animate = false;
    setTimeout(() => {
      modal.show = false;
    }, 300);
  }

  const saveExpense = () => {
    expenses.value.push({
      ...expense,
      id: uid()
    });

    closeModal();

    Object.assign(expense, {
      name: '',
      amount: '',
      category: '',
      id: null,
      date: Date.now()
    })
  }
</script>

<template>
  <div
    :class="{fix: modal.show}"
  >
    <header>
      <h1>Expense Planner</h1>
      
      <div class="header-container container shadow">
        <Budget 
          v-if="budget === 0"
          @set-budget="setBudget"
        />

        <BudgetControl
          v-else
          :budget="budget"
          :available="available"
        />
      </div>
      
    </header>

    <main v-if="budget > 0">
      
      <div class="container expense-list">
        <h2>{{ expenses.length > 0 ? "Expenses" : "There aren't any expenses"}}</h2>

        <Expense 
          v-for="expense in expenses"
          :key="expense.id"
          :expense="expense"
        />
      </div>

      <div 
        class="create-budget"
        @click="showModal"
      >
        <img 
          :src="newBudgetIcon" 
          alt="New budget icon"
        />
      </div>

      <Modal 
        v-if="modal.show"
        @close-modal="closeModal"
        @save-expense="saveExpense"
        :modal="modal"
        v-model:name="expense.name"
        v-model:amount="expense.amount"
        v-model:category="expense.category"
      />

    </main>
  </div>
</template>

<style> 
  :root {
    --azul: #3b82f6;
    --blanco: #FFF;
    --gris-claro: #F5F5F5;
    --gris: #94a3b8;
    --gris-oscuro: #64748b;
    --negro: #000;
  }

  html {
    font-size: 62.5%;
    box-sizing: border-box;
  }

  *,
  *:before,
  *:after {
    box-sizing: inherit;
  }

  body {
    font-size: 1.6rem;
    font-family: "Lato", sans-serif;
    background-color: var(--gris-claro);
  }

  h1 {
    font-size: 4rem;
  }

  h2 {
    font-size: 3rem;
  }

  .fix {
    overflow: hidden;
    height: 100vh;
  }

  header {
    background-color: var(--azul);
  }

  header h1 {
    padding: 3rem 0;
    margin: 0;
    color: var(--blanco);
    text-align: center;
  }

  .container {
    width: 90%;
    max-width: 80rem;
    margin: 0 auto;
  }

  .header-container {
    margin-top: -5rem;
    transform: translateY(5rem);
    padding: 5rem;
  }

  .shadow {
    box-shadow: 0px 10px 15px -3px rgba(0,0,0,0.1);
    background-color: var(--blanco);
    border-radius: 1.2rem;
    padding: 5rem;
  }

  .create-budget {
    position: fixed;
    bottom: 5rem;
    right: 5rem;
  }

  .create-budget img {
    width: 5rem;
    cursor:pointer;
  }

  .expense-list {
    margin-top: 10rem;
  }

  .expense-list h2 {
    text-align: center;
    font-weight: 900;
    color: var(--gris-oscuro);
  }
</style>