<template>
  <div class="container mb-5 mt-4 bg-secondary border-information">
    <div class="row">
      <div class="align-items-center">
        <p><strong>Total Spent:</strong> <span class="text-warning">-€ {{ totalSpent }}</span></p>
      </div>
      <div v-for="(spentCategory, index) in spentRatioByCategory" :key="index" class="align-items-center">
        <p class="noMargin"><strong>{{ spentCategory.category }}:</strong> <span class="text-info">{{ spentCategory.ratio }}%</span></p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SpentDetails',
  props: {
    spentRatioByCategory: {
      type: Array
    },
    totalSpent: {
      type: Number
    }
  },
}
</script>

<style scoped>
  .border-information {
    border-radius: 0.25rem;
    padding: 0.375rem 0.75rem;
  }

  .noMargin {
    padding: 0;
    margin: 0;
  }
</style>
