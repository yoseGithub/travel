<template>
    <div>
        <city-header :cities="cities"></city-header>
        <city-list :cities="cities" :hotCities="hotCities" :letter="letter"></city-list>
        <city-alphabet :cities="cities" @change="handleLetterChange"></city-alphabet>
    </div>
</template>

<script>
import CityHeader from './components/Header'
import CityList from './components/List'
import CityAlphabet from './components/Alphabet'
import axios from 'axios'

export default {
    name: "City",
    components: {
        CityHeader,
        CityList,
        CityAlphabet
    },
    data () {
        return {
            cities: {},
            hotCities: [],
            letter: ''
        }
    },
    methods: {
        getCityInfo () {
            axios.get('api/city.json')
                .then(this.handleGetCityInfuSucc)
        },
        handleGetCityInfuSucc (res) {
            res = res.data
            if (res.ret && res.data) {
                const data = res.data
                this.cities = data.cities
                this.hotCities = data.hotCities
            }
        },
        handleLetterChange (letter) {
            this.letter = letter
        }
    },
    mounted () {
        this.getCityInfo();
    }
}
</script>

<style lang="stylus" scoped>

</style>
