<template>
 <div class='search'>
  <h1>Search</h1>
  <button>Go</button>
  <input type='text' v-model='query' @keyup='getResult(query)'>
   <table class="table">
  <thead class="thead-primary">
  </thead>
  <tbody>
    <tr li v-for=" (casecountry, index) in cases" :key="index">
       <td >{{casecountry.Country}}</td>
      <td>{{casecountry.TotalConfirmed}}</td>
      <td>{{casecountry.TotalDeaths}}</td>
      <td>{{casecountry.TotalRecovered}}</td>
    </tr>
  </tbody>
    </table>
  
  </div>

</template>
<script>
import axios from 'axios'
export default {
  name: 'search',
  props: [],
  data () {
    return {
      query : '',
      results : ''
    }
      found: false
  },

   methods: {
  getResult(query) {
   axios.get(`https://api.covid19api.com/country/${country}`)
   .then(res =>  { found: true;
   this.results = res.data})
    console.log(this.results)
   }
 }
}
</script>