<template>
  <div class="container">
    <div class="row">
      <ul class="list-group">
        <li v-for="(spentItem, index) in spentList" :key="index" class="list-group-item list-group-item-info">
          <div class="row">
            <div class="col-2"><p class="text-danger">-€ {{ spentItem.spent }}</p></div>
            <div class="col-2"><p class="text-dark">{{ spentItem.category }}</p></div>
            <div class="col-8"><p class="text-dark">{{ spentItem.comment }}</p></div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script scoped>
export default {
  name: 'SpentList',
  props: {
    spentList: {
      type: Array,
      require: false
    }
  }
}
</script>
