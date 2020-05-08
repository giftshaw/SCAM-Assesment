<template>
  <div id="app">
    <div>
        <h2>Global statistics</h2>
        <table class="table table-hover">
  <thead>
    <tr>
      <th scope="col">Total Confirmed Cases</th>
      <th scope="col">Total Recovery Cases</th>
      <th scope="col">Total Deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>{{stats.TotalConfirmed}}</td>
      <td>{{stats.TotalRecovered}}</td>
      <td>{{stats.TotalDeaths}}</td>
    </tr>
    </tbody>
    </table>
    
    </div>

    <br>
    <!-- <div style="margin: 3% 30%">
      <ejs-autocomplete :dataSource="dataItem" :fields="dataFields" :query="dataQuery"
       placeholder="Search for country" >

    </ejs-autocomplete>
    </div> -->

    <input class="search" type="text" v-model="search" placeholder="search for country">
    
    
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
    <tr li v-for=" (casecountry, index) in filteredCases" :key="index">
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
import Vue from 'vue';
//auto complete vue plugin;
// import { AutoCompletePlugin } from '@syncfusion/ej2-vue-dropdowns';
// import {dataManager, webApiAdaptor} from '@syncfusion/ej2-data';
// import {Query} from '@syncfusion/ej2-data';
// Vue.use(AutoCompletePlugin);
export default {
  name: 'App',

    data(){
      return {
        cases: [],
        stats: [],
        search: ''
        // dataItem : new dataManager({
        //   url : 'https://api.covid19api.com/summary',
        //   adaptor : new webApiAdaptor, 
        //   crossDomain : true
        // }),

        // dataFields: {value: 'Country'},
        // dataQuery: new Query().select(['Country']).take(9).requiresCount,
      }
    },

    async created(){
          let fetchSummary = await axios.get('https://api.covid19api.com/summary')
            console.log(fetchSummary.data.Countries[0]);
            this.stats = fetchSummary.data.Global;
            console.log(this.stats);
            this.cases = fetchSummary.data.Countries;
          
      },
      computed:{
        filteredCases: function(){
          return this.cases.filter((casecountry) =>{
            return casecountry.Country.match(this.search);
          });
        }

    },
      
    
  components: {
   
  }
}
</script>

<style>

.search{
  float: right;
  margin: 2% auto;
}
</style>