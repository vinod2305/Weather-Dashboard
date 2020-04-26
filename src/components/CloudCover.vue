<template>
  <div class="frame">
  <div class="heading">
    <div class="text">Cloud Cover</div>
  </div>
  <div class="content">
    <div class="cloud-icon">
      <span class="iconify" data-icon="bi:cloud-fill" data-inline="false"></span>
    </div>
    <div class="cloud-data">{{parseInt(currently.cloudCover * 100)}}%</div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'CloudCover',
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
  font-size: 20px;
  
  .cloud-icon{
    margin-top: 10px;
    font-size: 230px;
    color: #9bccf1;
  }
  .cloud-data{
    margin-top: -80px;
    transform: translateY(-20px);
    font-size: 38px;
    font-weight: 800;
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
  font-size: 20px;
  
  .cloud-icon{
    margin-top: 10px;
    font-size: 130px;
    color: #9bccf1;
  }
  .cloud-data{
    margin-top: -50px;
    margin-bottom: 30px;
    font-size: 30px;
    font-weight: 800;
  }
}
}
</style>
