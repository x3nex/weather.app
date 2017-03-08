<template>
	<div>
		<h1>Hourly</h1>

		<div v-for="(item,index) in hourly " v-if="index<=7">

			<h2>{{ item.dt_txt }}</h2>
			<p>{{ item.main.temp | round }} </p>
			<p> {{ item.weather[0].description}}</p>
			<img :src="'http://openweathermap.org/img/w/' + item.weather[0].icon + '.png'" alt="">
		</div>
	</div>
</template>

<script>

	import axios from 'axios'

	export default {
		name: 'hourly-weather',
		data: function(){
			return {
				temp: '',
				icon: '',
				desc: '',
				hourly: []
				

			}
		},
		mounted(){

			axios.get('http://api.openweathermap.org/data/2.5/forecast', {
				params: {
					q: 'Belgrade,RS',
					appid: 'b138aca5f679afcd22a1961e66aa5709',
					units: 'metric'
				}
			})
			.then(response =>{
				this.hourly = response.data.list




			})
		},
			filters: {
			round: function (data){
				return Math.round(data);
			}
		}}


</script>

<style lang="scss" scoped>

</style>





<!-- <template>
    <div>
        <h1>Hourly</h1>
        <h3>06:00 <br>
        {{temp | round}}&#8451;<br>
       	<div class="icon2">{{icon}}</div>
        {{desc}}</h3>  
        <h3>09:00 <br>
        {{temp | round}}&#8451;<br>
       	<div class="icon2">{{icon}}</div>
        {{desc}}</h3>
        <h3>12:00</h3>
        <h3>15:00</h3>
        <h3>18:00</h3>
        <h3>21:00</h3>
        <h3>00:00</h3>
        
    </div>
</template>

<script>
import axios from 'axios'

    export default {
      name: 'hourly-weather',
      data: function(){
			return {
				temp: '',
				icon: '',
				desc: ''
			}
		},
		mounted(){
			axios.get('http://api.openweathermap.org/data/2.5/forecast', {
				params: {
					q: 'Belgrade,RS',
					appid: 'b138aca5f679afcd22a1961e66aa5709',
					units: 'metric'  			
				}
			})
			.then(response =>{
				this.temp = response.data.list[2].main.temp;
				this.icon = $(".icon2").html("<img src='http://openweathermap.org/img/w/" + response.data.list[2].weather[0].icon + ".png' alt='Icon depicting current weather.'>");
				this.desc = response.data.list[2].weather.description;

			});
		},
		
		filters: {
			round: function (data){
				return Math.round(data);
			}
		}}
    
</script>

<style>

</style> -->