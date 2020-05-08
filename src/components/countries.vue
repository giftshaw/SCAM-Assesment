<template>
  <div id="app">
    <table class="table">
  <thead class="thead-dark">
    <tr>
      <th scope="col">Country</th>
      <th scope="col">Total Confirmed Cases</th>
      <th scope="col">Total Deaths Cases</th>
      <th scope="col">Total Recovered Cases</th>
    </tr>
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


import axios from 'axios';

export default {
  name: 'App',
  props : [],
    data(){
      return {
        cases: [],
      }
    },

    methods:{
      

    },

    async created(){
          let fetchSummary = await axios.get('https://api.covid19api.com/summary')
            console.log(fetchSummary.data.Countries[0]);
            this.cases = fetchSummary.data.Countries;
      },


}
</script>

<style>

</style>