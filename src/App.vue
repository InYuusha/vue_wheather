<template>
<div id="app" :class=" typeof wheather.main!='undefined'&&wheather.main.temp>20?'warm':'cold'" >
  <main>
    <div class="search-box">
      <input type="text" class="search-bar" placeholder="Search" v-model="search" v-on:keypress="fetchWheather">
      <div class="wheather-wrap" v-if="typeof wheather.main!='undefined'">
        <div class="location-box">
          <div class="location">{{wheather.name}}, {{wheather.sys.country}}</div>
          <div class="date">{{currentTime()}}</div>
        </div>
        <div class="wheather-box">
          <div class="temp">{{Math.round(wheather.main.temp)}}°</div>
          <div class="wheather">{{wheather.weather[0].main}}</div>
        </div>
      </div>
    </div>
  </main>

</div>

</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      api_key:"81213429ad3d0b44c99689bc13d62cd3",
      url_base:"https://api.openweathermap.org/data/2.5/",
      search:"",
      wheather:{},
      
    }
  },
  methods:{
    fetchWheather(k){
      if(k.key=="Enter"){
        fetch(`${this.url_base}weather?q=${this.search}&units=metric&APPID=${this.api_key}`)
          .then(res =>{
            return res.json();
          }).then(this.setResults);
      }
    },
    setResults(results){
      this.wheather=results;
      console.log(this.wheather)
    },

    currentTime(){
      let d=new Date();
      let months=['Jan','Feb','March','April','May','June','July','Aug','Sept','Oct','Nov','Dec'];
      let days=['Sun','Mon','Tues','Wed','Thud','Fri','Sat'];

      let month=months[d.getMonth()];
      let day=days[d.getDay()];
      let year=d.getFullYear();
      let date=d.getDate()

      return `${day} ${date}, ${month}, ${year}`

     
    }

  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;

}
body{
  font-family:'montserrat', sans-serif;
 
 
}
#app.cold {
   background-image: url("https://image.freepik.com/free-vector/winter-landscape-concept-flat-design_23-2148360956.jpg");
   background-size: 700px 700px;
   background-position:bottom;
   background-repeat:no-repeat;
  
}
#app.warm{
  background-image:url("https://image.freepik.com/free-vector/realistic-blue-sky-with-clouds-composition-rays-sun-peek-out-from-clouds_1284-33934.jpg");
    background-size: 700px 700px;
   background-position:bottom;
   background-repeat:no-repeat;
}


main{
  min-height:100vh;
  background:linear-gradient(to bottom ,rgba(0,0,0,0.005),rgba(0,0,0,0.75));

}
.search-bar{
  padding:10px;
  box-shadow: 0 0 8px rgba(0,0,0,0.2);
  margin:20px;
  width:50vh;
  border-radius:0 14px 0 14px;
  background:rgba(255,255,255,0.6);
  border:none;
}

.search-box .search-bar:focus{
  box-shadow:0 0 8px rgba(0,0,0,0.6);
  border-radius:14px 0 14px 0;

}
.wheather-wrap{
  color:whitesmoke;
  margin-top:50px;
}
.temp{
  font-size:100px;
  padding:5px;
  margin:30px;
  display:inline-block;
  background:rgba(255,255,255,0.25);
  font-weight:900;
  border-radius:16px;
  box-shadow:0 8px rgba(0,0,0,0.2)

}

.location{
  font-size:35px;
}
.date{
  margin-top:10px;
}
.wheather{
  font-size:40px;
  font-weight:700;
}

</style>
