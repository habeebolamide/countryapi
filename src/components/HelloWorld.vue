<template>
  <div class="hello">
    <div class="container my-5">
      <div class="row">
        <div class="col-md-6"></div>
        <div class="col-md-6"></div>
      </div>
      <div class="row">
        <div class="col-md-3 my-2 " v-for="(c,i) in countries" :key="i">
          <div class="card">
            <img class="card-img-top" :src="c.flags.png" :alt="c.flags.alt">
            <div class="card-body">
              <h5 class="card-title text-left">{{c.name.common}}</h5>
              <p class="card-text text-left"><b>Population:</b> {{ c.population.toLocaleString() }}</p>
              <p class="card-text text-left"><b>Region:</b> {{ c.region }}</p>
              <p class="card-text text-left"><b>Capital: </b>
                <span v-for="(cap ,i) in c.capital" :key="i">{{ cap }}</span> </p>
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
  props: {
    msg: String
  },
  data(){
    return {
      countries:{}
    }
  },

  methods:{
    getCountry(){
      axios.get('https://restcountries.com/v3.1/all')
      .then((res) => {
        this.countries = res.data
      })
    }
  },
  mounted(){
    this.getCountry()
  }
}
</script>


<style scoped>
  .card-img-top{
    min-height: 150px;
    max-height: 150px;
  }
  .card-title{
    font-size: 15px;
    font-weight: 900;
  }
  .card-text {
    font-size: 15px;
  }
</style>
