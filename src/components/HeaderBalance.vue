<template>
  <div class="container">
    <div class="row">
      <div class="flex-row align-items-center">
        <h1 class="text-info">Balance:</h1>
        <p class="balance">€ {{ balance }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HeaderBalance',
  props: ['balance']
}
</script>

<style scoped>
  .flex-row {
    display: flex;
  }

  .balance {
    font-size: 24px;
    margin: 0;
    padding-left: 16px;
  }
</style>
