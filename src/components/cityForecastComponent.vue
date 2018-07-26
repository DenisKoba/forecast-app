<template>
    <div>
        <div class="forecast">
            <div v-for="element in currentData.weather" :class="element.description" class="forecast__background"></div>
            <multiselect
                    v-model="value"
                    :options="listOfCities"
                    label="name"
                    :searchable="true"
                    :close-on-select="false"
                    :show-labels="false"
                    @input="getCurrentData(), getCityData()"
                    placeholder="Pick a value">
            </multiselect>
            <div class="forecast__city-name">{{value.name}}</div>
            <div class="forecast__current-temperature">{{currentData.main.temp_max}}°C</div>
            <div class="forecast__current-descr">
                <span v-for="(i, index) in currentData.weather" :key="index">{{i.description }}</span>
            </div>
            <div class="forecast__timely-wrapper">
                <weather-timely
                        :cityData="cityData"
                        :item="item"
                        v-for="(item, index) in cityData.list"
                        :key="index">
                </weather-timely>
            </div>
        </div>
    </div>
</template>

<script>
    import vue from 'vue'
    import axios from 'axios'
    import weatherTimely from './weatherTimely'
    import Multiselect from 'vue-multiselect'
    import citiesList from './citiesList'

    vue.use(Multiselect)
    vue.use(axios)

    export default {
        components: {
            weatherTimely,
            Multiselect,
        },
        data() {
            return {
                listOfCities: citiesList,
                value: {
                    name: "Hurzuf,ua"
                },
                cityData: [],
                currentData: [],
            }
        },
        created() {
            this.getCityData()
            this.getCurrentData()
        },
        methods: {
            getCityData(){
                axios.get('https://api.openweathermap.org/data/2.5/forecast?q=' + this.value.name + '&units=metric&APPID=65b6075ccebccb206697e4659a3b9e26').then(response => {
                    this.cityData = response.data
                })
            },
            getCurrentData(){
                axios.get('https://api.openweathermap.org/data/2.5/weather?q=' + this.value.name + '&units=metric&APPID=65b6075ccebccb206697e4659a3b9e26').then(response => {
                    this.currentData = response.data
                })
            }
        }
    }
</script>

<style scoped lang="scss">

    .forecast {
        font-family: "Helvetica Neue", sans-serif;
        max-width: 500px;
        margin: 20px auto;
        display: block;
        height: calc(100vh - 60px);
        padding: 10px;
        box-shadow: 0 0 17px 5px #0000006b;
        overflow: scroll;
        color: #fff;
        background-color: #080808a3;
        &__background{
            position: fixed;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            z-index: -1;
        }
        &__city-name {
            text-align: center;
            font-size: 3em;
            padding: 2em 0 0 0;
            font-weight: 200;
        }
        &__current-temperature {
            font-size: 5em;
            text-align: center;
            color: #efebea;
        }
        &__timely-wrapper {
            display: flex;
            overflow: scroll;
            background: transparent;
            padding: 30px 0;
            margin: 10px;
        }
        &__current-descr {
            text-align: center;
            font-size: 20px;
            text-transform: uppercase;
            color: #d2d2d2;
        }
    }

    @media (max-width: 414px) {
        .forecast {
            height: 100vh;
            margin: 0;
            padding: 0;
        }
    }
</style>