<template>
  <div class="frame">
    <div class="heading">
      <div class="text">Wind</div>
    </div>
    <div class="content">
      <div class="speed">
        <div class="speed-icon">
          <span class="iconify" data-icon="wi:cloudy-gusts" data-inline="false"></span>
        </div>
        <div class="speed-title title">Speed</div>
        <div class="data speed-data">{{this.currently.windSpeed}} mph</div>
      </div>
      <div class="gust">
        <div class="gust-icon">
          <span class="iconify" data-icon="bx:bx-wind" data-inline="false"></span>
        </div>
        <div class="gust-title title">Gust</div>
        <div class="data gust-data">{{this.currently.windGust}} mph</div>
      </div>
      <div class="direction">
        <div class="direction-icon">
          <span class="iconify" data-icon="wi:wind-direction-ne" data-inline="false"></span>
        </div>
        <div class="direction-title title">Direction</div>
        <div class="data direction-data">{{this.degToCompass(this.currently.windBearing)}}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "WindStats",
  props: ["currently"],
  methods: {
    degToCompass(angle) {
      const directions = [
        "↑ N",
        "↗ NE",
        "→ E",
        "↘ SE",
        "↓ S",
        "↙ SW",
        "← W",
        "↖ NW"
      ];
      return directions[Math.round(angle / 45) % 8];
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

.content {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  font-size: 20px;

  .iconify {
    font-size: 40px;
    color: #6495ed;
  }
  .title {
    font-weight: 600;
  }
  .data {
    color: #808080;
  }
  .speed {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-direction: row;
    margin-top: 50px;
  }

  .gust {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-direction: row;
    margin-top: 40px;
  }
  .direction {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-direction: row;
    margin-top: 40px;
  }
}
@media only screen and (max-width: 1215px) {
  .frame {
    width: 100%;
    height: 100%;
    background: #fbfbff;
    box-shadow: 1px 2px 10px 0 rgba(0, 0, 0, 0.3);
    font-family: "Nunito Sans", sans-serif;
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

  .content {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    font-size: 20px;

    .iconify {
      font-size: 40px;
      color: #6495ed;
    }
    .title {
      font-weight: 600;
    }
    .data {
      color: #808080;
    }
    .speed {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-around;
      flex-direction: row;
      margin-top: 50px;
    }

    .gust {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-around;
      flex-direction: row;
      margin-top: 40px;
    }
    .direction {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-around;
      flex-direction: row;
      margin-top: 40px;
    }
  }
}
</style>
