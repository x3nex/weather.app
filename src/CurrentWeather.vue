<template>
    <div>

        <h1>{{temp | round}}&#8451;</h1>
        <div class="icon">{{icon}}</div>
        <h3>City: {{city}}</h3>
        <h4>Discription: {{desc}}</h4>
    </div>
</template>

<script>

import axios from 'axios'
  
  export default {
  	

    name: 'current-weather', 
  	data: function(){
			return {
				temp: '',
				city: '',
				desc: '',
				icon: ''
			}
		},
		mounted(){
			axios.get('http://api.openweathermap.org/data/2.5/weather', {
				params: {
					q: 'Belgrade,RS',
					appid: 'b138aca5f679afcd22a1961e66aa5709',
					units: 'metric'  			
				}
			})
			.then(response =>{
				this.temp = response.data.main.temp;
				this.city = response.data.name;
				this.desc = response.data.weather[0].description;
				this.icon = $(".icon").html("<img src='http://openweathermap.org/img/w/" + response.data.weather[0].icon + ".png' alt='Icon depicting current weather.'>");
			});
		},
		filters: {
			round: function (data){
				return Math.round(data);
			}
		}}
</script>

<style lang="scss">

$color: green;
h1 {
	color: $color
}

</style>

