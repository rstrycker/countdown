
<template>
     <div class="countdown">
         <template v-if="movie">
            <div class="block">
                <p class="digit">{{days}}</p>
                <p class="text">Days</p>
            </div>
            <div class="block">
                <p class="digit">{{hours | two_digits }}</p>
                <p class="text">Hours</p>
            </div>
            <div class="block">
                    <p class="digit">{{ minutes | two_digits }}</p>
                    <p class="text">Minutes</p>
            </div>
            <div class="block">
                <p class="digit">{{ seconds | two_digits }}</p>
                <p class="text">Seconds</p>
            </div>
        </template>
        <template v-else>
            <h1 class="error">
                Go ahead and select a movie
            </h1>
        </template>
    </div> 
</template>

<script>

export default {
    
    props:{
        movie: {
            required: true,
            type: Object
        }
    }, 
    filters: {
        two_digits: function (value) {
            if (value < 0) {
                return '00';
            }
            if (value.toString().length <= 1) {
                return ' ' + value;
            }
            return value;
        }
    },
    mounted: function mounted() {
        setInterval( () => {
          this.now = Math.trunc(new Date().getTime() / 1000);
        }, 1000);
    },
    data(){
        return{
            now: null
        }
    },
    created(){
        this.now = Math.trunc(new Date().getTime() / 1000)
    },
    computed: {
        movieName: function movieName(){
        return this.movie.title
        },
        dateInMilliseconds() {
        return Math.trunc(Date.parse(this.movie.date) / 1000);
        },
        seconds: function seconds() {
        return (this.dateInMilliseconds - this.now) % 60;
        },
        minutes: function minutes() {
        return Math.trunc((this.dateInMilliseconds - this.now) / 60) % 60;
        },
        hours: function hours() {
        return Math.trunc((this.dateInMilliseconds - this.now) / 60 / 60) % 24;
        },
        days: function days() {
        return Math.trunc((this.dateInMilliseconds - this.now) / 60 / 60 / 24);
        }
    }
}

</script>

<style>

    h1.error {
        font-family: Arial, Helvetica, sans-serif;
        font-size: initial;
        color: white;
    }

</style>
