<template>
  <div id="app" class="container-fluid">

    <SpentDetails
      v-bind:spent-ratio-by-category="spentRatioByCategory"
      v-bind:total-spent="totalSpent"
    />

    <HeaderBalance v-bind:balance="balance" />

    <div class="container">
      <div class="row">

        <div v-if="hasError" class="alert alert-danger" @click="clearErrors">
          <ErrorBox
            v-bind:positive-spent="errorType.positiveSpent"
            v-bind:no-category="errorType.noCategory"
            v-bind:no-balance="errorType.noBalance"
          />
        </div>

        <form @submit.prevent="addBalance">
          <div class="input-group mb-3">
            <div class="w-25 p-1">
              <input type="number" class="form-control" placeholder="€ 0" v-model="spent" />
            </div>
            <div class="p-1 select-options">
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

    <SpentList v-bind:spent-list="spentList"/>
  </div>
</template>

<script>
import HeaderBalance from "./components/HeaderBalance";
import ErrorBox from "./components/ErrorBox";
import SpentList from "./components/SpentList";
import SpentDetails from "./components/SpentDetails";

export default {
  name: 'App',
  components: {
    SpentDetails,
    SpentList,
    ErrorBox,
    HeaderBalance
  },
  data() {
    return {
      balance: 1000,
      spent: 0,
      totalSpent: 0,
      category: '',
      comment: '',
      hasError: false,
      errorType: {
        positiveSpent: false,
        noCategory: false,
        noBalance: false
      },
      spentList: [],
      spentRatioByCategory: []
    }
  },
  methods: {
    addBalance: function () {
      const { spent, category, comment, balance, spentList } = this
      let spentValue = parseInt(spent)

      this.errorType.positiveSpent = spentValue <=0
      this.errorType.noCategory = !category
      this.errorType.noBalance = spentValue > balance

      this.hasError = this.errorType.positiveSpent ||
                      this.errorType.noCategory ||
                      this.errorType.noBalance

      if (!this.hasError) {
        this.balance -= spentValue
        this.totalSpent += spentValue

        spentList.push({
          spent: spentValue,
          category,
          comment,
        })

        //Reset input values
        this.category = ''
        this.spent = ''
        this.comment = ''

        //Reset any error message
        this.clearErrors()

        //Adjust spent ratio
        this.updateSpentRatio()
      }
    },
    clearErrors: function () {
      this.hasError = false
      this.errorType.positiveSpent = false
      this.errorType.noCategory = false
      this.errorType.noBalance = false
    },
    updateSpentRatio: function () {
      const { spentList, totalSpent } = this;
      const spentRatioByCategory = Array.from(
        spentList.reduce((map, {category, spent}) =>
          map.set(category, (map.get(category) || 0) + spent), new Map),
        ([category, spent]) => ({
          category,
          ratio: Math.round((spent/totalSpent)*100)
        })
      )

      this.spentRatioByCategory = spentRatioByCategory;
    }
  }
}
</script>

<style scoped>
  .flex {
    display: flex;
  }

  select {
    border-radius: 0.25rem !important;
    height: 100%;
  }
</style>
