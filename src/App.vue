<template>
  <div id="app" class="container-fluid">

    <div class="container">
      <div class="row">
        <div class="flex-row align-items-center">
          <h1 class="text-info">Balance:</h1>
          <p class="balance">€ {{ balance - totalSpent }}</p>
        </div>
      </div>
    </div>

    <div class="container">
      <div class="row">
        <div v-if="hasError" class="alert alert-danger" @click="hasError = !hasError">
          <strong>Error:</strong> Please verify value, selected category or balance
        </div>
        <form @submit.prevent="addBalance">
          <div class="input-group mb-3">
            <div class="w-25 p-1">
              <input type="number" class="form-control" placeholder="€ 0" v-model="spent" />
            </div>
            <div class="p-1">
              <select class="select-options" v-model="category">
                <option disabled value="">Category</option>
                <option value="Housing">Housing</option>
                <option value="Food">Food</option>
                <option value="Insurance">Insurance</option>
                <option value="Transportation">Transportation</option>
                <option value="Taxes">Taxes</option>
              </select>
            </div>
            <div class="w-25 p-1">
              <input type="text" class="form-control" placeholder="Comment..." v-model="comment" />
            </div>
            <div class="input-group-append flex justify-content-center align-items-center p-1">
              <button>
                <i class="fa fa-plus" arial-hidden="true"></i>
              </button>
            </div>
          </div>
        </form>
      </div>
    </div>

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
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      balance: 1000,
      spent: 0,
      totalSpent: 0,
      category: '',
      comment: '',
      hasError: false,
      spentList: []
    }
  },
  methods: {
    addBalance: function () {
      const { spent, category, comment, balance, spentList } = this
      let totalSpent = parseInt(this.totalSpent) + parseInt(spent)

      if (spent <= 0 || !category || totalSpent > balance) {
        this.hasError = true;
      } else {
        this.totalSpent = totalSpent

        spentList.push({
          spent,
          category,
          comment
        })
      }
    }
  }
}
</script>

<style>
  .flex {
    display: flex;
  }

  .flex-row {
    display: flex;
  }

  .balance {
    font-size: 24px;
    margin: 0;
    padding-left: 16px;
  }

  .select-options {
    border-radius: 0.25rem !important;
    height: 100%;
  }
</style>
