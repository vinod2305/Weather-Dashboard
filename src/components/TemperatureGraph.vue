<template>
  <div class="temperature">
      <div class="heading">
        <div class="text">Temperature</div>
      </div>
    <line-chart class="graph" v-if="dataload" :chart-data="chartData" :chart-labels="chartLabels" ></line-chart>
  </div>


  
</template>



<script>
  import LineChart from '@/components/LineChart'
export default {
  name: 'TemperatureGraph',
  props: ['hourly'],
   components: {
      LineChart,
    },
  data () {
      return {
        chartLabels : [],
        chartData : [],
        dataload : false,
        window: {
            width: 0,
            height: 0
        }
      }
    },
    mounted () {
      this.dataAcess();
    },
    methods:{
      dataAcess(){

      for(var i=0;i < 9; i++){
        this.chartData.push(parseInt(this.hourly.data[i].temperature));
        this.chartLabels.push(this.unix_timeconvertor(this.hourly.data[i].time));
      }
      this.dataload = true;
    },
    unix_timeconvertor(UNIX_timestamp){
      var a = new Date(UNIX_timestamp * 1000);
      var hour = a.getHours().toString();
      var min = a.getMinutes().toString();
      if (hour.length == 1)
        hour = '0'+hour
      if (min.length == 1)
        min = '0'+min
      var info= hour + ':' + min 
      return this.tConvert(info);
},
    tConvert (time24) {
      var ts = time24;
      var H = +ts.substr(0, 2);
      var h = (H % 12) || 12;
      h = (h < 10)?("0"+h):h;  
      var ampm = H < 12 ? " AM" : " PM";
      ts = h + ts.substr(2, 3) + ampm;
      return ts;
    }
    }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.temperature{
    background: #fbfbff;
    box-shadow: 1px 2px 10px 0 rgba(0,0,0,0.3);
    
    .heading{
        width: 100%;
        height: 100px;
        font-size: 40px;
        background: #ffffff;
        text-align: left;
        font-family: 'Nunito Sans', sans-serif;
        box-shadow: 0 5px 4px -6px black;
        display: flex;
        align-items: center;
        justify-content: left;
        
    }
    .text{
    padding-left: 0.6em;
  }

    .graph{
      margin: 50px;

    }
}
@media only screen and (max-width: 1215px) {
  #line-chart{
        width: 100px !important;

    }
  .temperature{
    background: #fbfbff;
    box-shadow: 1px 2px 10px 0 rgba(0,0,0,0.3);
    
    .heading{
        width: 100%;
        height: 70px;
        font-size: 25px;
        background: #ffffff;
        text-align: left;
        font-family: 'Nunito Sans', sans-serif;
        box-shadow: 0 5px 4px -6px black;
        display: flex;
        align-items: center;
        justify-content: left;
        
    }
    .text{
    padding-left: 0.6em;
  }
    .graph{
      margin: 10px;
      
    }
    #line-chart{
        width: 100px !important;

    }
}
}
</style>
