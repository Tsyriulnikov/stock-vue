<script setup lang="ts">

</script>

<template>
  <div class="stock">
    <div class="stock-item" v-for="value in stock" :key="value.stock">
      <div class="stock-item_info">
        <div class="stock-item_cover">
          <img :src="value.image" alt="logo company">
        </div>
        <h3 class="stock-item_title">
          {{value.companyName}}
          <span>AAPL</span>
        </h3>
      </div>
      <span class="stock-item_price">{{value.price}} $</span>
    </div>
  </div>
  <h3>Get Info</h3>
  <select v-model="selected">
    <option value="" disabled>Select Company</option>
    <option v-for="value in stock" :key="value.stock" :value="value.description">{{ value.companyName }}</option>
  </select>
  <div class="info">
    {{ selected }}
  </div>
</template>

<script lang="ts">
import axios from "axios";
import {defineComponent} from "vue";

export default defineComponent({
  name: 'Stocks',
  data() {
    return {
      stock: [],
      errors: [],
      selected: ''
    }
  },
  created() {
    axios.get('https://financialmodelingprep.com/api/v3/profile/NVDA?apikey=dd7c82edc0907c1da536d6d646c43e44')
    // axios.get('https://financialmodelingprep.com/api/v3/profile/AAPL,NVDA,TSLA,AMD,INTC,MDB,SPCE,V,DAL,DOCU,OKTA,AMZN,PINS,TRIP,GDDY,DIS,MCD,NOK,UPWK,IBM,FB,ZM,OZON,NFLX,EA,HLT,H,CCL?apikey=6c9be8fcb7df7894ba5ae48be14935fc')
        .then(response => {
          this.stock = response.data
          console.log(response)
        })
        .catch(e => {
          this.errors.push(e)
        })
  }
})
</script>