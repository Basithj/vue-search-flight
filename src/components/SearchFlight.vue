<template>
  <div class="search-box-container text-left">
        <b-form @submit="onSubmit" v-if="show">
          <h3>Book Flight</h3>
          <br/>
          <b-form-group label="Origin:">
            <autocomplete
              :search="search"
              placeholder="Search origin"
              aria-label="Search origin"
              :get-result-value="getOriginResultValue"
            ></autocomplete>
          </b-form-group>
          <b-form-group label="Destination:">
            <autocomplete
              :search="search"
              placeholder="Search destination"
              aria-label="Search destination"
              :get-result-value="getDestinationResultValue"
            ></autocomplete>
          </b-form-group>
          <b-form-group label="Aircraft:">
            <b-form-select v-model="selected_airlines" :options="airlines" size="sm" class="mt-3">
              <template v-slot:first>
                <b-form-select-option :value="null" disabled hidden>-- Select Aircraft --</b-form-select-option>
              </template>
            </b-form-select>
          </b-form-group>
          <b-form-group id="input-group-2" label="Passenger:" label-for="input-2">
            <b-form-input
              id="input-2"
              v-model="passenger"
              type="number"
              required
              placeholder="How Many Passenger"
            ></b-form-input>
          </b-form-group>
          <b-form-group label="Desired Date:">
            <b-form-input
              id="input-1"
              v-model="desiredDate"
              type="date"
              required
            ></b-form-input>
          </b-form-group>

          <b-button
            variant="primary"
            @click="showSummary"
          >
            Summary
          </b-button>
        </b-form>
        <FlightSummary
          v-if="!show"
          :origin="origin"
          :destination="destination"
          :aircraft="selected_airlines"
          :passenger="passenger"
          :desireddate="desiredDate"
        />
  </div>
</template>

<script>

import Autocomplete from '@trevoreyre/autocomplete-vue'
import FlightSummary from '@/components/FlightSummary.vue'
import '@trevoreyre/autocomplete-vue/dist/style.css'

export default {
  name: 'SearchFlight',
  components: {
    Autocomplete,
    FlightSummary
  },
  data() {
    return {
      show:true,
      destination:null,
      origin:null,
      desiredDate:null,
      airports:[],
      selected_airlines: null,
      passenger:null,
      airlines:[
          { value: 'Alaska Airlines', text: 'Alaska Airlines' },
          { value: 'Allegiant Air', text: 'Allegiant Air' },
          { value: 'American Airlines', text: 'American Airlines' },
          { value: 'Alaska Airlines', text: 'Delta Air Lines' },
          { value: 'Allegiant Air', text: 'Frontier Airlines' },
          { value: 'American Airlines', text: 'Hawaiian Airlines' },
          { value: 'JetBlue', text: 'JetBlue' },
          { value: 'Southwest Airlines', text: 'Southwest Airlines' },
          { value: 'Spirit Airlines', text: 'Spirit Airlines' },
          { value: 'United Airlines', text: 'United Airlines' }
        ]
    }
  },
  methods:{
    search(input){
      return new Promise(resolve => {
        if (input.length < 3) { return resolve([]) }

        fetch("https://comeari-airportsfinder-v1.p.rapidapi.com/api/airports/by-text?text="+encodeURI(input), {
          "method": "GET",
          "headers": {
            "x-rapidapi-host": "cometari-airportsfinder-v1.p.rapidapi.com",
            "x-rapidapi-key": "4cbcc3738emsh31ae3c3614de1dep1b9556jsn6f4bed6a2cc9"
          }
        })
        .then(response => {
          return response.json()
        })
        .then(data => {
          resolve( data.filter(airport => {
              return airport.city.toLowerCase()
                .startsWith(input.toLowerCase())
          }))
        })
      })
    },
    onSubmit(evt) {
      evt.preventDefault()
    },
    getOriginResultValue(result) {
      this.origin = result.name
      return result.name
    },
    getDestinationResultValue(result) {
      this.destination = result.name
      return result.name
    },
    showSummary(){
      this.show = false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
