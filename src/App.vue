<template>
  <div class="container" :style="`background-image: url(${ selectedBackground });`">
    <movie-title class="wrap" :movie="selectedMovie"></movie-title> 
    
    <div class="selectblock"><select class="wrap" v-model="selected">
      <option disabled value="">Please select a movie</option>
      <option v-for="movie in movies" :value="movie.id" :key="movie.id">{{ movie.short_title }}</option>
    </select></div>

    <countdown :movie="selectedMovie"></countdown>
    
    

 </div>
</template>

<script>

import MovieTitle from "./components/Title.vue"
import Countdown from "./components/Countdown.vue"
//import VGauge from 'vgauge'

export default {
  name: 'app',
  components: {
    MovieTitle,
    Countdown
  },
  data(){
    return {
      gaugeOptions: {
        angle:0.15,
        colorStart:"#6FADCF",
        colorStop:"#8FC0DA",
        generateGradient:true,
        highDpiSupport:true,
        limitMax:false,
        limitMin:false,
        lineWidth:0.44,
        pointer: {
          color:"#000000",
          length:0.6,
          strokeWidth:0.035,
        },
        radiusScale:1,
        strokeColor:"#E0E0E0"
      },
      selected:null,
      movies: [{
        "title":"Spiderman: Far From Home",
        "date":"2019-07-02 19:00:00",
        "movieImage":"http://quickflashdesigns.com/countdown/spider-man-far-home.jpg",
        "id":1,
        "short_title":"Spiderman (2019)"
      },{
        "title":"Star Wars: The Rise of Skywalker",
        "date":"2019-12-19 19:00:00",
        "movieImage":"http://www.quickflashdesigns.com/countdown/star-wars-the-rise-of-skywalker.jpg",
        "id":2,
        "short_title":"Star Wars (2019)"
      },{
        "title":"Ant-Man and The Wasp",
        "date":"2018-07-05 19:00:00",
        "movieImage":"http://www.quickflashdesigns.com/countdown/AM2/Ant-Man2.jpg",
        "id":3,
        "short_title":"Ant-Man (2018)"
      },{
        "title":"Venom",
        "date":"2018-10-04 19:00:00",
        "movieImage":"http://www.quickflashdesigns.com/countdown/venom-movie-poster.jpg",
        "id":4,
        "short_title":"Venom (2018)"
      },{
        "title":"Spiderman: Into the Spiderverse",
        "date":"2018-12-13 19:00:00",
        "movieImage":"http://www.quickflashdesigns.com/countdown/spiderman-spiderverse.jpg",
        "id":5,
        "short_title":"Spiderman: Spiderverse (2018)"
      },{
        "title":"Captain Marvel",
        "date":"2018-03-07 19:00:00",
        "movieImage":"http://www.quickflashdesigns.com/countdown/CM/CaptMarvel.jpg",
        "id":6,
        "short_title":"Capt. Marvel"
      },{
        "title":"Deadpool 2",
        "date":"2018-05-17 19:00:00",
        "movieImage":"http://www.quickflashdesigns.com/countdown/DP2/deadpool-2.jpg",
        "id":7,
        "short_title":"Deadpool 2"
      }]
    };
  },

  computed: {
    selectedMovie() {
      return this.movies.find(movie => {
        return movie.id==this.selected
      })
    },
      selectedBackground(){
        const movie = this.selectedMovie;
        if (!movie){
          return "";
        }
        return movie.movieImage; 
      }
    
  }
}
</script>

<style>
@import url(https://fonts.googleapis.com/css?family=Roboto+Condensed:400|Roboto:100);

html,
body{
  padding: 0;
  margin:0;
  height: 100%;
}

#app {
  /* align-items: center;
  bottom: 0;
  background-color: #34495e;
  display: flex;
  justify-content: center;
  left: 0;
  position: relative;
  right: 0;
  top: 30; */
}

.wrap {
  display: block;
  margin: 0 auto;
}
.container{
    background: black  no-repeat center center fixed;
    background-size: cover;
    height: 100%;
}
.countdown {
  background-color:rgba(0, 0, 0, 0.5);
  text-align: center;
  flex-direction: column;
  margin: 0px;
}
.countdown {
  text-align: center;
  flex-direction:column;
  margin: 0px;
}
.title {
  text-align: center;
  flex-direction: row;
  margin: 20px;
}
.selectblock {
  text-align: center;
  flex-direction: row;
  margin: 20px;
}
.block {
  display: flex;
  flex-direction:row;
  margin: 20px;
}

.text {
  color: #1abc9c;
  font-size: 3vw;
  font-family: 'Roboto Condensed', serif;
  font-weight: 10;
  margin: 20px 20px, 10px, 20px;
  text-align: center;
  display: inline-block;
}
.digit {
  color: #ecf0f1;
  font-size: 8vw; 
  font-weight: 100;
  font-family: 'Roboto', serif;
  margin: 10px 5px 15px 35px;
  text-align: center;
}
.messagetext {
  color: #bc891a;
  font-size: 18px;
  font-family: 'Roboto Condensed', serif;
  font-weight: 40;
  margin-top: 10px;
  margin-bottom: 10px;
  text-align: center;
  font-style: italic;
}
.titletext {
  color: #1abc9c;
  font-size: 25px;
  font-family: 'Roboto Condensed', serif;
  font-weight: 40;
  margin-top: 0px;
  margin-bottom: 10px;
  text-align: center;
}



</style>
