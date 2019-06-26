
<template>
     <div class="countdown">
         <template v-if="movie">
            <div class="countdownblock">
                <span class="digit">{{days}}</span>
                <span class="text">Days</span>
            
                <span class="digit">{{hours | two_digits }}</span>
                <span class="text">Hours</span>
          
                <span class="digit">{{ minutes | two_digits }}</span>
                <span class="text">Minutes</span>
                    
                <span class="digit">{{ seconds | two_digits }}</span>
                <span class="text">Seconds</span>
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
        text-align: center;
    }

</style>
