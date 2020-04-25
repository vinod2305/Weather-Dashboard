<template>
  <div class="frame">
  <div class="heading">
    <div class="text">Current Conditions</div>
  </div>
  <div class="content">
    <div class="icon">
      <div v-if="this.currently.icon == 'clear-day'">
        <span class="iconify clear-day" data-icon="bx:bxs-sun" data-inline="false"></span>
      </div>
      <div v-else-if="this.currently.icon == 'clear-night'">
       <span class="iconify clear-night" data-icon="emojione:full-moon" data-inline="false"></span>
      </div>
      <div v-else-if="this.currently.icon == 'rain'">
        <span class="iconify rain" data-icon="emojione:cloud-with-rain" data-inline="false"></span>
      </div>
      <div v-else-if="this.currently.icon == 'snow'">
        <span class="iconify snow" data-icon="ion:snow" data-inline="false"></span>
      </div>
      <div v-else-if="this.currently.icon == 'wind'">
        <span class="iconify wind" data-icon="bx:bx-wind" data-inline="false"></span>
      </div>
      <div v-else-if="this.currently.icon == 'fog'">
        <span class="iconify fog" data-icon="twemoji:fog" data-inline="false"></span>
      </div>
      <div v-else-if="this.currently.icon == 'cloudy'">
        <span class="iconify cloudy" data-icon="emojione:cloud" data-inline="false"></span>
      </div>
      <div v-else-if="this.currently.icon == 'partly-cloudy-day'">
        <span class="iconify partly-cloudy-day" data-icon="emojione:sun-behind-cloud" data-inline="false"></span>
      </div>
      <div v-else-if="this.currently.icon == 'partly-cloudy-night'">
        <span class="iconify partly-cloudy-night" data-icon="ion:cloudy-night-sharp" data-inline="false"></span>
      </div>
      <div v-else-if="this.currently.icon == 'thunderstorm'">
        <span class="iconify thunderstorm" data-icon="emojione:cloud-with-lightning-and-rain" data-inline="false"></span>
      </div>
      <div v-else-if="this.currently.icon == 'tornado'">
        <span class="iconify tornado" data-icon="emojione-monotone:tornado" data-inline="false"></span>
      </div>        
    </div>
    <div class="weather">{{this.currently.summary}}</div>
    <div class="temperature"> {{parseInt(this.currently.temperature)}}°</div>
    <div class="apparenttemperature"> Feels like {{parseInt(this.currently.apparentTemperature)}}°</div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'CurrentCondition',
  props: ['currently']
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
  font-size: 35px;
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
  
  .clear-day{
    font-size: 140px;
    margin-top: 20px;
    color: #f9d71c;
    text-shadow: 2px 2px 5px #f9d71c;
  }
  
  .weather{
    font-size: 23px;
    margin-top: 10px;
    
  }
  
  .temperature{
    font-size: 80px;
  }
  .apparenttemperature{
    font-size: 20px;
    color: #808080;
    margin-top: -12px;
  }
  .clear-day{
      color: #f9d71c;
      text-shadow: 2px 2px 5px #f9d71c;
    }
    
    .clear-night{
      
    }
    
    .rain{
      
    }
    .snow{
      color: #76c9d7;
      text-shadow: 2px 2px 5px #76c9d7;
    }
    .wind{
      color: #2a80e3;
    }
    .fog{
      
    }
    .cloudy{
      
    }
    .partly-cloudy-night{
      color: #b8c1d2;
    }
    .partly-cloudy-day{
      
    }
    .thunderstorm{
      
    }
    .tornado{
      
    }
    
  
    .iconify{
      font-size: 120px;
      margin-top: 20px;
      text-shadow: 2px 2px 5px #f9d71c;
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
  
  .clear-day{
    font-size: 140px;
    margin-top: 20px;
    color: #f9d71c;
    text-shadow: 2px 2px 5px #f9d71c;
  }
  
  .weather{
    font-size: 23px;
    margin-top: -10px;
    
  }
  
  .temperature{
    margin-top: -15px;
    font-size: 80px;
  }
  .apparenttemperature{
    font-size: 20px;
    color: #808080;
    margin-top: -18px;
  }
  .clear-day{
      color: #f9d71c;
      text-shadow: 2px 2px 5px #f9d71c;
    }
    
    .clear-night{
      
    }
    
    .rain{
      
    }
    .snow{
      color: #76c9d7;
      text-shadow: 2px 2px 5px #76c9d7;
    }
    .wind{
      color: #2a80e3;
    }
    .fog{
      
    }
    .cloudy{
      
    }
    .partly-cloudy-night{
      color: #b8c1d2;
    }
    .partly-cloudy-day{
      
    }
    .thunderstorm{
      
    }
    .tornado{
      
    }
    
  
    .iconify{
      font-size: 120px;
      margin-top: 10px;
      text-shadow: 2px 2px 5px #f9d71c;
    }
}
}
</style>
