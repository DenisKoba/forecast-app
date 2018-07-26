<template>
    <div class="timely">
        <span class="timely__time">{{item.dt_txt}}</span>
        <p class="timely__temperature">{{item.main.temp}}°C</p>
        <p class="timely__descr" v-for="i in item.weather">{{i.description}}</p>
        <img class="timely__icon" v-for="i in item.weather" :src="'http://openweathermap.org/img/w/'+ i.icon + '.png'">
    </div>
</template>

<script>
    export default {
        name: 'weasther-timely',
        props: ['cityData', 'item'],
        data() {
            return {
            }
        }
    }
</script>

<style scoped lang="scss">
    .timely{
        padding: 10px;
        min-width: 60px;
        &__time{
            font-size: 10px;
            line-height: 12px;
            text-align: left;
            display: block;
         }
        &__temperature{
            padding: 10px 0;
            color: #ffffff;
            font-weight: 600;
        }
        &__descr{
            font-size: 14px;
            min-height: 40px;
        }
    }
</style>