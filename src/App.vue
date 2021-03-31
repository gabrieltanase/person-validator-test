<template>
  <div id="app">
    <PersonDetails v-if="person" :person="person"/>
    <p v-else class="msg">Person data is not matching the Schema!</p>
  </div>
</template>

<script>

import _ from 'lodash';
import PersonDetails from './components/PersonDetails.vue'

import { IPersonDetails } from './models/person';

export default {
  name: 'App',
  components: {
    PersonDetails
  },
  data() {
    return { 
      person: this.validatePersonData(this.fetchDataFromApi()),
      message: null 
    }
  },
  methods: {
    /**  
     * Fetch the data from backend (dummy data)
    */
    fetchDataFromApi() {
      return {
        name: 'James', 
        age: 22,
        siblings: ['Johnnathan', 'Bjørn'],
        metaData: {},
        active: true,
      }
    },
  
    /** 
     * Validates person data that comes from API for consistancy 
     * @param data - person details 
     * @returns Object - personDetails matched data against person details schema
     * @returns unmatching data message
    */
    validatePersonData(data) {
      if (!data) {
        return;
      }
      // Define the person schema
      const personSchema = IPersonDetails

      /** Iterate data and check each property against the schema types 
       * stops the iteration when
      */
      const check = _.every(data, (value, key) => {
        /**
         * exception for Array
         * check if the value is an array against same property from schema object 
         */ 
        if (_.isArray(value) && personSchema[key] === 'array') {
          return true;
        }
        return typeof value === personSchema[key];
      });
      
      console.log(check);
      return check ? data : null;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.msg {
  text-align: center;
  color: red;
  font-weight: bold;
}
</style>
