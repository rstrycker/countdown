<template>
    <div class="titletext" v-if="movie">
        <div>
            {{movieName}}
        </div>
        <div>
            {{movieDate}}
        </div>
        <div class="messagetext">
            {{message}}
        </div>
    </div>
</template>

<script>

export default {
    props:{
        movie: {
            default: () => {},
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
    computed: {
        movieName() {
            const movie = this.movie
            if (!movie) return false
            return movie.title;
        },
        movieDate() {
            const movie = this.movie
            if (!movie) return false

            let a = new Date(movie.date);
            var months = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
            var year = a.getFullYear();
            var month = months[a.getMonth()];
            var date = a.getDate();
            var hour = a.getHours();
            if (hour>12) {
                hour=hour-12;
                var suffix="PM";
            } else {
                var suffix="AM"
            }
            var min = a.getMinutes();
            if (min <= 0) {
                min="00";
            }
            var sec = a.getSeconds();
            if (sec <= 0) {
                sec="00";
            }
            var time = month + ' ' + date + ' ' + year + ' - ' + hour + ':' + min + ':' + sec + " " + suffix;
            return time;

        },
        message: function message(){
            const movie = this.movie
            if (!movie) return false

            //return Math.trunc(new Date().getTime() / 1000);
            if ((Math.trunc(Date.parse(movie.date) / 1000) - Math.trunc(new Date().getTime() / 1000))<0){
                return "This movie has already been released";
            } else {
                return "";
            }
        }
    }

}
</script>