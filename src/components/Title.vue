<template>
    <div class="titletext">
        <div>
            {{movieName}}
        </div>
        <div>
            {{movieDate}}
        </div>
        <div>
            {{message}}
        </div>
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
       computed: {
        movieName: function movieName(){
        return this.movie.title;
        },
        movieDate: function movieDate(){
            var a = new Date(this.movie.date);
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
            //year=this.movie.date.getHours();
            //return year;
        },
        message: function message(){
            //return Math.trunc(new Date().getTime() / 1000);
            if ((Math.trunc(Date.parse(this.movie.date) / 1000) - Math.trunc(new Date().getTime() / 1000))<0){
                return "This movie has already been released";
            } else {
                return "";
            }
        }
    }

}
</script>