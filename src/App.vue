<template>
  <div id="app" class="container-fluid">

    <div class="container">
      <div class="row">
        <div class="flex-row align-items-center">
          <h1 class="text-info">Balance:</h1>
          <p class="balance">€ {{ balance }}</p>
        </div>
      </div>
    </div>

    <div class="container">
      <div class="row">
        <form>
          <div class="input-group mb-3">
            <div class="w-25 p-1">
              <input type="number" class="form-control" placeholder="€ 0" />
            </div>
            <div class="p-1">
              <select class="select-options">
                <option selected>Category</option>
                <option value="Housing">Housing</option>
                <option value="Food">Food</option>
                <option value="Insurance">Insurance</option>
                <option value="Transportation">Transportation</option>
                <option value="Taxes">Taxes</option>
              </select>
            </div>
            <div class="w-25 p-1">
              <input type="text" class="form-control" placeholder="Comment..." />
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
          <li class="list-group-item list-group-item-info">
            <div class="row">
              <div class="col-2"><p class="text-danger">-€ 100</p></div>
              <div class="col-2"><p class="text-dark">Housing</p></div>
              <div class="col-8"><p class="text-dark">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc mattis sollicitudin elit, at laoreet nunc rhoncus non. Phasellus facilisis pretium dolor eget rhoncus. Nullam nec felis tristique, iaculis massa et, scelerisque nulla. Fusce eros mi, varius et suscipit sit amet, fermentum vel sem.</p></div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data() {
    return {
      balance: 1000
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
