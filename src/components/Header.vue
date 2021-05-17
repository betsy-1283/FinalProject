<template>
  <div class="container">
    <h1>Weather for Your Area</h1>
    <form class="form-inline">
      <input
        type="text"
        class="form-control mb-2 mr-sm-2"
        id="inlineFormInputZip"
        placeholder="Enter Zip Code"
        v-model="query"
      />
      <select class="custom-select" id="format">
        <option selected>Choose...</option>
        <option value="metric">Celsius</option>
        <option value="imperial">Farenheit</option>
        
      </select>

      <button type="button" class="btn btn-primary mb-2"  v-on:click="myFunc">Submit</button>
      <p id="results"></p>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Header',
  data()
  {
   return{
     userzip: "",
     userformat: ""


   }
  },
  methods: {
    myFunc() {
    //alert(document.getElementById("inlineFormInputZip").value);
      //console.log(document.getElementById("format").value);
      this.userzip = document.getElementById("inlineFormInputZip").value;
      this.userformat = document.getElementById("format").value;
      console.log(this.userzip);
      console.log(this.userformat);


    }

  },
  mounted()
  {
    axios.get("https://api.openweathermap.org/data/2.5/weather?zip=65721,us&appid=44cd4a31de2da1cbc8a7f43996818092")
    .then((response) => {
      console.log(response.data);
      console.log(response.data.weather[0].description)

      


      


    })
  }


};
</script>

<style scoped>
    .custom-select, #inlineFormInputZip, button{
        padding: 5px;
        margin: 10px;
    }
</style>
