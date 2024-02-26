<template>
  <div class="hello">
    <div class="container-fluid my-5">
      <div class="row my-5">
        <div class="col-md-4 ">
          <input type="text" v-model="filters.search" @keyup="Search()" placeholder="Search for a country ..." class="form-control py-4">
        </div>
        <div class="col-md-2 ml-auto">
          <select class="form-control" style="height: 3rem;" v-model="filters.region" @change="Search" aria-label="Default select example">
            <option selected value="Filter By Region">Filter By Region</option>
            <option value="Africa">Africa</option>
            <option value="Americas">America</option>
            <option value="Asia">Asia</option>
            <option value="Europe">Europe</option>
            <option value="Oceania">Oceania</option>
          </select>
        </div>
      </div>
      <div class="row">
        <div class="col-md-3 my-2 " v-for="(c, i) in countries" :key="i">
          <div class="card">
            <img class="card-img-top" :src="c.flags.png" :alt="c.flags.alt">
            <div class="card-body">
              <h5 class="card-title text-left">{{ c.name.common }}</h5>
              <p class="card-text text-left"><b>Population:</b> {{ c.population.toLocaleString() }}</p>
              <p class="card-text text-left"><b>Region:</b> {{ c.region }}</p>
              <p class="card-text text-left"><b>Capital: </b>
                <span v-for="(cap, i) in c.capital" :key="i">{{ cap }}</span>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data() {
    return {
      countries: {},
      filcountries: {},
      filters: {
        region: "Filter By Region"
      }
    }
  },

  methods: {
    getCountry() {
      axios.get('https://restcountries.com/v3.1/all')
        .then((res) => {
          this.countries = res.data
          this.filcountries = res
        })
    },
    Search() {
      this.countries = this.filcountries.data.filter((country) => {
        // return console.log(country);
        if (this.filters.search && this.filters.region != "Filter By Region") {
          return country.region == this.filters.region && country.name.common == this.filters.search;
        }
        if (this.filters.search) {
          console.log("Search term:", this.filters.search);
          console.log("Country name:", country.name.common.toLowerCase());
          return country.name.common.toLowerCase() == this.filters.search.toLowerCase();
        }
        if (this.filters.region != "Filter By Region") {
          return country.region == this.filters.region;
        }
        return true;
      });


    }
  },
  mounted() {
    this.getCountry()
  }
}
</script>


<style scoped>
.card-img-top {
  min-height: 150px;
  max-height: 150px;
}

.card-title {
  font-size: 15px;
  font-weight: 900;
}

.card-text {
  font-size: 15px;
}
</style>
