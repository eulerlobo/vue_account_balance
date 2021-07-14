<template>
  <div>
    <div v-if="positiveSpent">
      <strong>Error:</strong> Don't input negative value for the spend just the absolute value of it
    </div>
    <div v-if="noCategory">
      <strong>Error:</strong> Please select a category
    </div>
    <div v-if="noBalance">
      <strong>Error:</strong> You don't have enough balance to spend
    </div>
  </div>
</template>
git a
<script scoped>
export default {
  name: 'ErrorBox',
  props: ['positiveSpent', 'noCategory', 'noBalance']
}
</script>
