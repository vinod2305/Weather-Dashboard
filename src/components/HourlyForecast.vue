<template>
  <div class="frame" v-if="this.dataload == true">
    <div class="heading">
      <div class="text">Hourly Forecast</div>
    </div>
    <div class="contenthourly">
      <div v-for="item in this.timedata" :key="item.id">
        <div class="content1 content-box">
          <div class="time">{{item.times}}</div>

          <div class="icon">
            <div v-if="item.timeIcon == 'clear-day' ">
              <span class="iconify clear-day" data-icon="bx:bxs-sun" data-inline="false"></span>
            </div>
            <div v-else-if="item.timeIcon == 'partly-cloudy-day'">
              <span
                class="iconify partly-cloudy-day"
                data-icon="emojione:sun-behind-cloud"
                data-inline="false"
              ></span>
            </div>
            <div v-else-if="item.timeIcon == 'clear-night'">
              <span class="iconify clear-night" data-icon="emojione:full-moon" data-inline="false"></span>
            </div>
            <div v-else-if="item.timeIcon == 'rain'">
              <span class="iconify rain" data-icon="emojione:cloud-with-rain" data-inline="false"></span>
            </div>
            <div v-else-if="item.timeIcon == 'snow'">
              <span class="iconify snow" data-icon="ion:snow" data-inline="false"></span>
            </div>
            <div v-else-if="item.timeIcon == 'wind'">
              <span class="iconify wind" data-icon="bx:bx-wind" data-inline="false"></span>
            </div>
            <div v-else-if="item.timeIcon == 'fog'">
              <span class="iconify fog" data-icon="twemoji:fog" data-inline="false"></span>
            </div>
            <div v-else-if="item.timeIcon == 'cloudy'">
              <span class="iconify cloudy" data-icon="emojione:cloud" data-inline="false"></span>
            </div>
            <div v-else-if="item.timeIcon == 'partly-cloudy-day'">
              <span
                class="iconify partly-cloudy-day"
                data-icon="emojione:sun-behind-cloud"
                data-inline="false"
              ></span>
            </div>
            <div v-else-if="item.timeIcon == 'partly-cloudy-night'">
              <span
                class="iconify partly-cloudy-night"
                data-icon="ion:cloudy-night-sharp"
                data-inline="false"
              ></span>
            </div>
            <div v-else-if="item.timeIcon == 'thunderstorm'">
              <span
                class="iconify thunderstorm"
                data-icon="emojione:cloud-with-lightning-and-rain"
                data-inline="false"
              ></span>
            </div>
            <div v-else-if="item.timeIcon == 'tornado'">
              <span
                class="iconify tornado"
                data-icon="emojione-monotone:tornado"
                data-inline="false"
              ></span>
            </div>
          </div>
          <div class="summary">{{item.summary}}</div>
          <div class="temperature">{{item.temp}}°</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment-timezone";

export default {
  name: "HourlyForecast",
  props: ["hourly", "location"],
  mounted() {
    this.dataAcess();
  },
  data() {
    return {
      timedata: [],
      dataload: false
    };
  },
  methods: {
    dataAcess() {
      for (var i = 1; i < 7; i++) {
        this.timedata.push({
          times: this.unix_timeconvertor(this.hourly.data[i].time),
          timeIcon: this.hourly.data[i].icon,
          temp: parseInt(this.hourly.data[i].temperature),
          summary: this.hourly.data[i].summary
        });
      }
      this.dataload = true;
    },
    unix_timeconvertor(UNIX_timestamp) {
      var time = moment
        .unix(UNIX_timestamp)
        .tz(this.location.timezone)
        .format("h A");
      return time;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.frame {
  width: 100%;
  height: 100%;
  background: #fbfbff;
  box-shadow: 1px 2px 10px 0 rgba(0, 0, 0, 0.3);
  font-family: "Nunito Sans", sans-serif;
}

.heading {
  height: 100px;
  background: #ffff;
  font-size: 40px;
  text-align: left;
  box-shadow: 0 5px 4px -6px black;
  display: flex;
  align-items: center;
  justify-content: left;

  .text {
    padding-left: 0.6em;
  }
}

.contenthourly {
  display: flex;
  align-items: center;
  justify-content: space-around;
  flex-direction: row;

  .content-box {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;

    .clear-day {
      color: #f9d71c;
      text-shadow: 2px 2px 5px #f9d71c;
    }

    .clear-night {
    }

    .rain {
    }
    .snow {
      color: #76c9d7;
      text-shadow: 2px 2px 5px #76c9d7;
    }
    .wind {
      color: #2a80e3;
    }
    .fog {
    }
    .cloudy {
    }
    .partly-cloudy-night {
      color: #b8c1d2;
    }
    .partly-cloudy-day {
    }
    .thunderstorm {
    }
    .tornado {
    }

    .material-icons {
      font-size: 120px;
      margin-top: 20px;
    }
    .iconify {
      font-size: 120px;
      margin-top: 20px;
      text-shadow: 2px 2px 5px #f9d71c;
    }
    .time {
      margin-top: 20px;
      font-size: 20px;
      text-align: center;
    }
    .temperature {
      font-size: 50px;
      margin-top: 20px;
      text-align: center;
    }
  }
}

@media only screen and (max-width: 1215px) {
  .frame {
    width: 100%;
    height: 100%;
    background: #fbfbff;
    box-shadow: 1px 2px 10px 0 rgba(0, 0, 0, 0.3);
    font-family: "Nunito Sans", sans-serif;
    margin: auto;
  }

  .heading {
    height: 70px;
    background: #ffff;
    font-size: 25px;
    text-align: left;
    box-shadow: 0 5px 4px -6px black;
    display: flex;
    align-items: center;
    justify-content: left;

    .text {
      padding-left: 0.6em;
    }
  }

  .contenthourly {
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-direction: column;

    .content-box {
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;

      .clear-day {
        color: #f9d71c;
        text-shadow: 2px 2px 5px #f9d71c;
      }

      .clear-night {
      }

      .rain {
      }
      .snow {
        color: #76c9d7;
        text-shadow: 2px 2px 5px #76c9d7;
      }
      .wind {
        color: #2a80e3;
      }
      .fog {
      }
      .cloudy {
      }
      .partly-cloudy-night {
        color: #b8c1d2;
      }
      .partly-cloudy-day {
      }
      .thunderstorm {
      }
      .tornado {
      }

      .material-icons {
        font-size: 100px;
        margin-top: 20px;
      }
      .iconify {
        font-size: 100px;
        margin-top: 2px;
        text-shadow: 2px 2px 5px #f9d71c;
      }
      .time {
        margin-top: 20px;
        font-size: 20px;
        text-align: center;
        font-weight: 600;
      }
      .temperature {
        font-size: 30px;
        margin-top: 2px;
        margin-bottom: 20px;
        text-align: center;
      }
    }
  }
}
</style>
