<template>
  <div class="topnav">
      <div class="grid-container">
      <div class="time"><div class="text">{{this.info}}</div></div>
      <div class="location">{{this.location.city}}  <span class="state">{{this.location.state}} {{this.location.country.toUpperCase()}}</span></div>
</div>
</div>



</template>

<script>
import moment from 'moment-timezone'

export default {
  name: 'NavBar',
  props: ['currently', 'location'],
   mounted(){
       this.dataAcess();
  },
  data(){
    return{
      timedata : [],
      dataload : false,
      info : '',
    }
  },
  methods:{
      dataAcess(){
          this.info =this.unix_timeconvertor(this.currently.time);
          this.dataload = true
      },

      unix_timeconvertor(UNIX_timestamp){
      var time = moment
          .unix(UNIX_timestamp)
          .tz(this.location.timezone)
          .format('Do MMMM YYYY •  h:mma');
        return time;  

    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.topnav {
  background-color: #ffffff;
  overflow: hidden;
  border-bottom: .8px solid #ececf0;
  width: 100%;
  
    
}


.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1.2fr 0.8fr;
  grid-template-rows: 1fr ;
  gap: 1px 1px;
  grid-template-areas: "time time time location" ;
  padding: 30px;
  width: 100%
}
.text{
        font-family: 'Nunito Sans', sans-serif;
        font-size: 2.2vw;
        margin-left: 50px;
    }

.time { grid-area: time; }

.state{
    font-size: 1vw;
}

.location { 
  grid-area: location; 
  font-family: 'Nunito Sans', sans-serif;
  font-size: 2.2vw;
}

@media only screen and (max-width: 1215px) {
  *{
    width: 100%;
  }
  .topnav {
  background-color: #ffffff;
  overflow: hidden;
  border-bottom: .8px solid #ececf0;
  width: max-width;
  
    
}


.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1.8fr 0.2fr;
  grid-template-rows: 1fr ;
  gap: 1px 1px;
  grid-template-areas: "time time time location" ;
  padding: 10px;
}
.text{
        font-family: 'Nunito Sans', sans-serif;
        font-size: 15px;
        margin-left: 5px;
        
    }

.time { grid-area: time; 
display: flex;
    align-items: center;
    justify-content: left;
}

.state{
    font-size: 1vw;
    display: none;
}

.location { 
  grid-area: location; 
  font-family: 'Nunito Sans', sans-serif;
  font-size: 20px;
}
}
</style>
