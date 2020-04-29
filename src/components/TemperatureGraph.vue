<template>
  <div class="temperature">
    <div class="heading">
      <div class="text">Temperature</div>
    </div>
    <line-chart class="graph" v-if="dataload" :chart-data="chartData" :chart-labels="chartLabels"></line-chart>
  </div>
</template>



<script>
import LineChart from "@/components/LineChart";
import moment from "moment-timezone";

export default {
  name: "TemperatureGraph",
  props: ["hourly", "location"],
  components: {
    LineChart
  },
  data() {
    return {
      chartLabels: [],
      chartData: [],
      dataload: false,
      window: {
        width: 0,
        height: 0
      }
    };
  },
  mounted() {
    this.dataAcess();
  },
  methods: {
    dataAcess() {
      for (var i = 0; i < 9; i++) {
        this.chartData.push(parseInt(this.hourly.data[i].temperature));
        this.chartLabels.push(
          this.unix_timeconvertor(this.hourly.data[i].time)
        );
      }
      this.dataload = true;
    },
    unix_timeconvertor(UNIX_timestamp) {
      var time = moment
        .unix(UNIX_timestamp)
        .tz(this.location.timezone)
        .format("h:mm A");
      return time;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.temperature {
  background: #fbfbff;
  box-shadow: 1px 2px 10px 0 rgba(0, 0, 0, 0.3);

  .heading {
    width: 100%;
    height: 100px;
    font-size: 40px;
    background: #ffffff;
    text-align: left;
    font-family: "Nunito Sans", sans-serif;
    box-shadow: 0 5px 4px -6px black;
    display: flex;
    align-items: center;
    justify-content: left;
  }
  .text {
    padding-left: 0.6em;
  }

  .graph {
    margin: 50px;
  }
}
@media only screen and (max-width: 1215px) {
  #line-chart {
    width: 100px !important;
  }
  .temperature {
    background: #fbfbff;
    box-shadow: 1px 2px 10px 0 rgba(0, 0, 0, 0.3);

    .heading {
      width: 100%;
      height: 70px;
      font-size: 25px;
      background: #ffffff;
      text-align: left;
      font-family: "Nunito Sans", sans-serif;
      box-shadow: 0 5px 4px -6px black;
      display: flex;
      align-items: center;
      justify-content: left;
    }
    .text {
      padding-left: 0.6em;
    }
    .graph {
      margin: 10px;
    }
    #line-chart {
      width: 100px !important;
    }
  }
}
</style>
