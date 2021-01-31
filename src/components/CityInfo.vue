<template>
  <div>
    <div
      :style="{
        'background-image':
          'url(' + require(`../assets/${backgroundImage}.jpg`) + ')',
      }"
      id="cityBackground"
    ></div>
    <div id="cityInfo">
      <h1>{{ cityName }}</h1>
      Temperature: {{ temperature.temperature }}
    </div>
  </div>
</template>

<script>
export default {
  name: "CityInfo",
  props: {
    cityName: String,
    backgroundImage: String,
  },
  data: function () {
    return {
      temperature: null,
    };
  },
  methods: {
    async getTemperature() {
      const response = await fetch(
        `http://localhost:3000/${this.backgroundImage}`
      );
      this.temperature = await response.json();
    },
  },
  mounted() {
    this.getTemperature();
  },
};
</script>

<style>
#cityBackground {
  background-image: url("../assets/humpolec.jpg");
  background-size: cover;
  filter: blur(4px);
  position: absolute;
  width: 60%;
  height: 80%;
  left: 50%;
  margin-left: -30%;
}

#cityInfo {
  background: rgba(0, 0, 0, 0.3);
  position: absolute;
  border: 5px white solid;
  left: 50%;
  width: 40%;
  margin-left: -20%;
  top: 50%;
  height: 30%;
  margin-top: -7.5%;
  color: white;
  font-weight: bold;
  font-size: 28px;
  text-decoration: underline;
}
</style>