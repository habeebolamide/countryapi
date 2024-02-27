<template>
    <div class="hello">
        <div class="container-fluid my-5">
            <div class="row my-5">
                <div class="col-md-2 ">
                    <router-link to="/">
                        <button class="btn btn-transparent px-4"><ion-icon name="arrow-back-outline"></ion-icon>
                            Back</button>
                    </router-link>
                </div>
            </div>
            <div class="row my-5">
                <div class="col-md-6">
                    <img class="img-fluid" :src="country.flags.svg" alt="">
                </div>
                <div class="col-md-1"></div>
                <div class="col-md-5 my-auto">
                    <h3 class="text-left">{{ country.name.common }}</h3>
                    <div class="row">
                        <div class="col-md-6">
                            <p class="sub"><b>Native Name: </b>{{ country.name.official }}</p>
                            <p class="sub"><b>Population: </b>{{ country.population.toLocaleString() }}</p>
                            <p class="sub"><b>Regions: </b>{{ country.region }}</p>
                            <p class="sub"><b>Sub Region: </b>{{ country.subregion }}</p>
                            <p class="sub"><b>Captital: </b>
                                <span v-for="(cap, i) in country.capital" :key="i">{{ cap }}</span>
                            </p>
                        </div>
                        <div class="col-md-6">
                            <p class="sub"><b>Regions: </b>{{ country.region }}</p>
                            <p class="sub"><b>Currencies: </b>{{ currency }}</p>
                            <p class="sub"><b>Languages: </b>
                                <span v-for="(cap, i) in country.capital" :key="i">{{ cap }}</span>
                            </p>
                        </div>
                    </div>
                    <div class="bordercount float-left my-5">
                        <p><b>Border Countries: </b></p>
                        <ul>
                                <li v-for="(cap, i) in country.borders" class="borders" :key="i">{{ cap }}</li>
                            </ul>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>

<script>

export default {
    name: 'CountryDetails',
    data() {
        return {
            country: {},
            currency: ''
        }
    },
    props: {
        data: Object
    },
    methods: {

    },
    mounted() {
        this.country = JSON.parse(localStorage.getItem('countryData'));
        const dynamicKey = Object.keys(this.country.currencies)[0]
        this.currency = this.country.currencies[dynamicKey].name
        console.log(this.country);
    }
}
</script>

<style scoped>
.hello {
    height: 100vh;
}

.btn {
    background: var(--color-background-secondary);
    border: none;
    color: var(--color-text-primary);
    box-shadow: var(--color-boxshadow-primary) 0px 7px 29px 0px;
}

.sub {
    text-align: left;
    font-size: 15px;
}
.borders {
    font-size: 10px;
    margin-right: 1rem;
    background: var(--color-background-secondary);
    border: none;
    color: var(--color-text-primary);
    box-shadow: var(--color-boxshadow-primary) 0px 7px 29px 0px;
    display: inline-block; /* Change from inline to inline-block */
    padding-right: 2rem;
    padding-left: 2rem;
    padding-top: 0.2rem;
    padding-bottom: 0.2rem;
}
.bordercount {
    text-align: left;
    display: inline-block; /* Ensure the divs are inline */
}
.bordercount p {
    display: inline;
    margin-right: 0.5rem; /* Add margin between the <p> tag and the list */
}

</style>