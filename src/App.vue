<template>
 <div id="app">
  <div v-if="this.locationload">
    <div id="loader" class="center" v-if="loading"></div> 
    <div v-if="this.dataload == true" id="appdata">
      <NavBar class="navbar" v-bind:currently="currently" v-bind:location="location" />

      <div class="search">
        <div class="text">
          <input
            type="text"
            v-model="locationcity"
            ref="autocomplete"
            placeholder="Enter City ..."
            class="searchfield search-location"
            onfocus="value = ''"
          />
        </div>
        <div class="search-button">
          <button type="button" v-on:click="locationAcess" class="button">
            <i class="material-icons">search</i>
          </button>
        </div>
      </div>

    
        <div class="grid-container">
          <div class="Current-Conditions">
            <CurrentCondition class="currentcondition" v-bind:currently="currently" />
          </div>
          <div class="Hourly-Forecast">
            <HourlyForecast
              class="hourlyforecast"
              v-bind:hourly="hourly"
              v-bind:location="location"
            />
          </div>
          <div class="Temperature">
            <TemperatureGraph
              class="temperaturegraph"
              v-bind:hourly="hourly"
              v-bind:location="location"
            />
          </div>
          <div class="Today">
            <TodayStats class="todaystats" v-bind:daily="daily" v-bind:location="location" />
          </div>
          <div class="Wind">
            <WindStats class="windstats" v-bind:currently="currently" />
          </div>
          <div class="Cloud-Cover">
            <CloudCover class="cloudcover" v-bind:currently="currently" />
          </div>
        </div>
        </div>
     
    
  </div>
  <div class="search-bar" v-else>
    <div class="text" style="margin-top: 30%;">{{this.locationstatus}}
      <div>Please enter the city, you want to search about. </div>
    </div>
    <div class="search" style="margin-top: 20%;">
      <div class="text">
        <input
          type="text"
          v-model="locationcity"
          ref="autocomplete"
          placeholder="Enter City ..."
          class="searchfield search-location"
          onfocus="value = ''"
        />
      </div>
      <div class="search-button">
        <button type="button" v-on:click="locationAcess" class="button">
          <i class="material-icons">search</i>
        </button>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue from "vue";
import CurrentCondition from "@/components/CurrentCondition.vue";
import HourlyForecast from "@/components/HourlyForecast.vue";
import TemperatureGraph from "@/components/TemperatureGraph.vue";
import TodayStats from "@/components/TodayStats.vue";
import WindStats from "@/components/WindStats.vue";
import CloudCover from "@/components/CloudCover.vue";
import NavBar from "@/components/NavBar.vue";

export default {
  name: "App",
  components: {
    CurrentCondition,
    HourlyForecast,
    TemperatureGraph,
    CloudCover,
    WindStats,
    TodayStats,
    NavBar
  },
  mounted() {
    this.getLocation();
  },
  data() {
    return {
      currently: {},
      hourly: {},
      daily: {},
      dataload: false,
      latitude: 0,
      longitude: 0,
      location: {
        city: "",
        country: "",
        state: "",
        timezone: ""
      },
      locationcity: "",
      locationstatus: "",
      locationload: false,
      address: "",
      loading: true
    };
  },
  methods: {
    getLocation() {
      if (navigator.geolocation) {
        console.log(navigator.geolocation);
        navigator.geolocation.getCurrentPosition(
          this.showPosition,
          this.showError
        );
      }
    },
    showPosition(position) {
      this.latitude = position.coords.latitude.toFixed(4);
      this.longitude = position.coords.longitude.toFixed(4);
      this.requestData();
    },
    showError(error) {
      console.log(error);
      if (error.message.startsWith("Only secure origins are allowed")) {
        this.locationstatus = "Only secure origins are allowed";
        return;
      }
      switch (error.code) {
        case error.PERMISSION_DENIED:
          this.locationstatus = "User denied the request for Geolocation.";
          break;
        case error.POSITION_UNAVAILABLE:
          this.locationstatus = "Location information is unavailable.";
          break;
        case error.TIMEOUT:
          this.locationstatus = "The request to get user location timed out.";
          break;
        case error.UNKNOWN_ERROR:
          this.locationstatus = "An unknown error occurred.";
          break;
      }
    },
    requestData() {
      axios
        .get(
          "https://api.opencagedata.com/geocode/v1/json?q=" +
            this.latitude +
            "+" +
            this.longitude +
            "&key=e01586a1ad4f4909b38222a4a022c98b"
        )
        .then(response => {
          console.log(response.data);
          this.location.city = response.data.results[0].components.city;
          this.location.country =
            response.data.results[0].components.country_code;
          this.location.state = response.data.results[0].components.state_code;
          this.location.timezone =
            response.data.results[0].annotations.timezone.name;
          this.locationload = true;
          this.loading = false;
        })
        .catch(err => {
          this.errorMessage = err.response.data.error;
          this.showError = true;
        });
      axios
        .get(
          "https://csm.fusioncharts.com/files/assets/wb/wb-data.php?src=darksky&lat=" +
            this.latitude +
            "&long=" +
            this.longitude +
            "?units=si&exclude=hourly,flags,offset"
        )
        .then(response => {
          Vue.set(this.$data, "currently", response.data.currently);
          Vue.set(this.$data, "hourly", response.data.hourly);
          Vue.set(this.$data, "daily", response.data.daily);
          this.dataload = true;
        })
        .catch(err => {
          this.errorMessage = err.response.data.error;
          this.showError = true;
        });
    },
    locationAcess() {
      axios
        .get(
          "https://us1.locationiq.com/v1/search.php?key=879eff1bd6c48b&q=" +
            this.locationcity +
            "&format=json"
        )
        .then(response => {
          this.dataload = false;
          this.latitude = response.data[0].lat.substring(
            0,
            response.data[0].lat.length - 3
          );
          this.longitude = response.data[0].lon.substring(
            0,
            response.data[0].lon.length - 3
          );
          this.requestData();
          this.locationcity = "";
        })
        .catch(err => {
          this.errorMessage = err;
          this.showError = true;
        });
    }
  }
};
</script>

<style lang="scss">
#loader {
  border: 12px solid #f3f3f3;
  border-radius: 50%;
  border-top: 12px solid #444444;
  width: 80px;
  height: 80px;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  100% {
    transform: rotate(360deg);
  }
}

.center {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
}

.searchbar{
  width: 100%;
  height: 100%;
}
body {
  background: #fffafa;
  margin: 0;
}
#app {
  font-family: "Nunito Sans", sans-serif;
  text-align: center;
  color: #2c3e50;
  position: relative;
  background: #fffafa;
}

.mssg {
  font-family: "Nunito Sans", sans-serif;
  font-size: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.text {
  grid-area: text;
}

.search-button {
  grid-area: search-button;
}

.search {
  display: grid;
  grid-template-columns: 1fr 1fr 1.8fr 0.2fr;
  grid-template-rows: 1fr;
  gap: 1px 1px;
  grid-template-areas: "text text text search-button";
  width: 60%;
  margin-left: 20%;
  font-size: 0;
  background: #fff;
  border: 2px solid #7ad3f7;
  border-radius: 10px;
  padding: 5px;
  box-sizing: border-box;
  margin-bottom: 50px;

  .searchfield {
    font-family: "Nunito Sans", sans-serif;
    float: left;
    width: 100%;
    height: 100%;
    border-radius: 0;
    font-size: 23px;
    font-weight: 600;
    padding: 0 0 0 15px;
    background: #fff;
    color: #4d8dcb;
    border: 0;
    outline-width: 0;
  }
  .button {
    width: 100%;
    height: 100%;
    border: none;
    border-radius: 0;
    background: #fff;
    color: #5ca4ea;
    font-size: 20px;
    padding: 0;
    top: 3px;
    outline-width: 0;

    .material-icons {
      font-size: 40px;
      display: flex;
      align-items: center;
      justify-content: center;
    }
  }
}

.grid-container {
  display: grid;
  grid-template-columns: 1fr 0.4fr 1.4fr 1.2fr;
  grid-template-rows: 0.7fr 1fr 0.7fr;
  gap: 50px 50px;
  margin: 40px;
  grid-template-areas: "Current-Conditions Hourly-Forecast Hourly-Forecast Hourly-Forecast" "Temperature Temperature Temperature Temperature" "Today Today Wind Cloud-Cover";
}

.Current-Conditions {
  grid-area: Current-Conditions;
  transition: all 0.5s ease-in-out;
}

.Hourly-Forecast {
  grid-area: Hourly-Forecast;
  transition: all 0.5s ease-in-out;
}

.Temperature {
  grid-area: Temperature;
  transition: all 0.5s ease-in-out;
}

.Today {
  grid-area: Today;
  transition: all 0.5s ease-in-out;
}

.Wind {
  transition: all 0.5s ease-in-out;
  grid-area: Wind;
}

.Cloud-Cover {
  transition: all 0.5s ease-in-out;
  grid-area: Cloud-Cover;
}

.Current-Conditions:hover {
  transform: scale(1.015);
}
.Hourly-Forecast:hover {
  transform: scale(1.015);
}
.Temperature:hover {
  transform: scale(1.015);
}
.Today:hover {
  transform: scale(1.015);
}
.Wind:hover {
  transform: scale(1.015);
}
.Cloud-Cover:hover {
  transform: scale(1.015);
}

@media only screen and (max-width: 1215px) {
  .search {
    display: grid;
    grid-template-columns: 1fr 1fr 1.8fr 0.2fr;
    grid-template-rows: 1fr;
    gap: 1px 1px;
    grid-template-areas: "text text text search-button";
    width: 90%;
    margin-left: 5%;
    font-size: 0;
    background: #fff;
    border: 2px solid #7ad3f7;
    border-radius: 10px;
    padding: 1px;
    box-sizing: border-box;
    margin-bottom: 15px;

    .searchfield {
      font-family: "Nunito Sans", sans-serif;
      float: left;
      width: 100%;
      height: 100%;
      border-radius: 0;
      font-size: 13px;
      font-weight: 600;
      padding: 0 0 0 15px;
      background: #fff;
      color: #4d8dcb;
      border: 0;
      outline-width: 0;
    }
    .button {
      width: 100%;
      height: 100%;
      border: none;
      border-radius: 0;
      background: #fff;
      color: #5ca4ea;
      font-size: 20px;
      padding: 0;
      top: 3px;
      outline-width: 0;

      .material-icons {
        font-size: 30px;
        display: flex;
        align-items: center;
        justify-content: center;
      }
    }
  }

  #app {
    font-family: "Nunito Sans", sans-serif;
    text-align: center;
    color: #2c3e50;
    position: relative;
    width: 100%;
    background: #fffafa;
  }

  .grid-container {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 0.31fr 1.3fr 0.2fr 0.5fr 0.32fr 0.2fr;
    gap: 40px 10px;
    margin: 15px 15px 40px 15px;
    grid-template-areas: "Current-Conditions" "Hourly-Forecast" "Temperature" "Today" "Wind" "Cloud-Cover";
  }

  .Current-Conditions {
    grid-area: Current-Conditions;
    margin-right: 15px;
    margin-left: 15px;
  }

  .Hourly-Forecast {
    grid-area: Hourly-Forecast;
    width: 70%;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-left: 15%;
  }

  .Temperature {
    grid-area: Temperature;
    margin-right: 4px;
    margin-left: 4px;
  }

  .Today {
    grid-area: Today;
    width: 80%;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-left: 10%;
  }

  .Wind {
    grid-area: Wind;
    width: 70%;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-left: 15%;
  }

  .Cloud-Cover {
    grid-area: Cloud-Cover;
    width: 70%;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-left: 15%;
  }
}
</style>
