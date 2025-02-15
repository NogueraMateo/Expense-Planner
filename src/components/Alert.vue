<template>

  <div
    class="alert"
  >
    <slot></slot>
  </div>

</template>

<style scoped>
  .alert {
    padding: 1rem;
    font-weight: 900;
    text-align: center;
    text-transform: uppercase;
    font-size: 1.6rem;
    background-color: var(--blanco);
    color: #b91c1c;
    border-left: .5rem solid #b91c1c;
    margin-bottom: 2rem;
}
</style>