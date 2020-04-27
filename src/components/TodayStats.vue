<template>
  <div class="frame">
  <div class="heading">
    <div class="text">Today</div>
  </div>
  <div class="content">
    <div class="sun-time">
      <div class="sunrise">
        Sunrise
        <div class="sunrise-icon">
          <span class="iconify" data-icon="feather:sunrise" data-inline="false"></span>
        </div>
        <div class="sunrise-time">{{this.unix_timeconvertor(this.daily.data[0].sunriseTime)}}</div>
      </div>
      <div class="sunset">
        Sunset
        <div class="sunset-icon">
          <span class="iconify" data-icon="feather:sunset" data-inline="false"></span>
        </div>
        <div class="sunset-time">{{this.unix_timeconvertor(this.daily.data[0].sunsetTime)}}</div>
      </div>
    </div>
    <div class="stats">
      <div class="uv">UV
        <div class="pie pie-uv">
          <radial-progress-bar :diameter="130"
                       :completed-steps="this.daily.data[0].uvIndex"
                       :total-steps="10"
                       :startColor="startColor1"
                       :stopColor="stopColor1"
                       :innerStrokeColor="innerStrokeColor1"/>
          <p class="uv-text text">{{ this.daily.data[0].uvIndex }}/10</p>
        </div>  
      </div>
      <div class="visibility">Visibility
        <div class="pie pie-visibility">
          <radial-progress-bar :diameter="130"
                       :completed-steps="this.daily.data[0].visibility"
                       :total-steps="100"
                       :startColor="startColor"
                       :stopColor="stopColor"
                       :innerStrokeColor="innerStrokeColor"/>
          <p class="visibility-text text">{{ parseInt(this.daily.data[0].visibility) }} mi</p>              
        </div> 
      </div>
    </div>
  </div>
  </div>
  
    
</template>

<script>
import moment from 'moment-timezone'
import RadialProgressBar from 'vue-radial-progress'
export default {
  name: 'TodayStats',
  props: ['daily', 'location'],
  data () {
    return {
      startColor: "#1977f9",
      stopColor: "#1977f9",
      innerStrokeColor: "#aed3fd",
      startColor1: "#68c753",
      stopColor1: "#68c753",
      innerStrokeColor1: "#afebc9"
    }
  },
   components: {
    RadialProgressBar
  },
  methods:{
    unix_timeconvertor(UNIX_timestamp){
      var time = moment
          .unix(UNIX_timestamp)
          .tz(this.location.timezone)
          .format('h:mm A');
        return time;  
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.frame{ 
  width: 100%;
  height: 100%;
  background: #fbfbff;
  box-shadow: 1px 2px 10px 0 rgba(0,0,0,0.3);
  font-family: 'Nunito Sans', sans-serif;
}

.heading{
  height: 100px;
  background: #ffff;
  font-size: 40px;
  text-align: left;
  box-shadow: 0 5px 4px -6px black;
   display: flex;
  align-items: center;
  justify-content: left;
  
  .text{
   padding-left: 0.6em;
  }
}

.content{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  
  .sun-time{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-direction: row;
    margin-top: 20px;
    .sunrise{
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-around;
      flex-direction: column;
      color: 	#808080;
      .sunrise-icon{
        font-size: 40px;
        margin-top: 10px;
        color: #fece32;
      }
      .sunrise-time{
        font-weight: 600;
        font-size: 25px;
        color: #000000;
      }
    }
    .sunset{
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-around;
      flex-direction: column;
      color: #808080;
      .sunset-icon{
        font-size: 40px;
        margin-top: 10px;
        color: #fece32;
      }
      .sunset-time{
        font-weight: 600;
        font-size: 25px;
        color: #000000;
      }
    }
  }
  .stats{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-direction: row;
    margin-top: 20px;
    font-weight: 600;
    font-size: 20px;
    .uv{
      
    }
    .visibility{
      
    }
    .text{
      margin-top: -80px;
      
    }
  }
}

@media only screen and (max-width: 1215px) {
  .frame{ 
    width: 100%;
    height: 100%;
    background: #fbfbff;
    box-shadow: 1px 2px 10px 0 rgba(0,0,0,0.3);
    font-family: 'Nunito Sans', sans-serif;
  }

  .heading{
    height: 70px;
    background: #ffff;
    font-size: 25px;
    text-align: left;
    box-shadow: 0 5px 4px -6px black;
    display: flex;
    align-items: center;
    justify-content: left;
    
    .text{
      padding-left: 0.6em;
    }
  }

.content{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  
  .sun-time{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-direction: row;
    margin-top: 10px;
    .sunrise{
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-around;
      flex-direction: column;
      color: 	#808080;
      .sunrise-icon{
        font-size: 40px;
        margin-top: 10px;
        color: #fece32;
      }
      .sunrise-time{
        font-weight: 600;
        font-size: 20px;
        color: #000000;
      }
    }
    .sunset{
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-around;
      flex-direction: column;
      color: #808080;
      .sunset-icon{
        font-size: 40px;
        margin-top: 10px;
        color: #fece32;
      }
      .sunset-time{
        font-weight: 600;
        font-size: 20px;
        color: #000000;
      }
    }
  }
  .stats{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-direction: column;
    margin-top: 20px;
    font-weight: 600;
    font-size: 20px;
    .uv{
      
    }
    .visibility{
      margin-top: 50px;
    }
    .text{
      margin-top: -80px;
      
    }
  }
}
}
</style>
