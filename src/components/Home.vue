<style scoped>
	.home{
		width: 100%;
		height: 26rem;
		background-color: #0088CC;
	} 
	.home_aside{
	width: 40%;
	height: 100%;
	float: right;	
		background-color: #33CCCC;
	}
	.home_aside_ul{
		width:80%;

		margin: 0 auto;
	}
	.brand{
		width: 10rem;
		height: 10rem;
		background-color: red;
		display: inline-flex;
		flex-wrap:wrap;
		margin: 1rem;
		transform: translateX(10%);
	}
	.brand img{
		width: 10rem;
		height: 10rem;
	}
	.brand img:hover{
		transform:rotate(360deg);
		transition: all .5s ease;
	}
</style>
<template>
  <div class="home">
  	<aside class="home_aside" >
    <h1>welcome</h1>
 		<ul class="home_aside_ul">
 			<li v-for="brand in brands" class="brand" @click="changeShow(brand.name)"><img :src="brand.src"></li>
 				<router-link :to="'/home/'+brand.name" tag="img" :src="brand.src" :alt="brand.name" class="home_aside_ul_img"></router-link>
 		</ul>
 	</aside>
  	<transition name="introduction">
  		<router-view></router-view>
 	</transition>
 	
  </div>  
</template>

<script>
import {mapGetters} from 'vuex'
export default {
	data (){
		return {

		}
	},
	computed:{
		...mapGetters({
			hw:'getHW',
			brands:'getBrands'
		}),
		home_aside_height:function(){
			var a= parseInt(this.hw.h)-200;
			return a<389?389:a
		},
		home_aside_height_margin:function(){
			return parseInt(this.home_aside_height-300)/2
		}
	},
	methods:{
		changeShow(type){
			this.$store.dispatch('changeShow',type)
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	/*.home{min-width: 1150px;width:100%;}
	.home_aside{width: 400px;float: right;margin:0;background: #00BC9B}
	.home:after{display: block;content: "";clear:both;width: 0;height: 0}
	.home_aside h1{text-align: center;font-family: TrashHand;font-size: 32px;
color:darkslateblue;}
	.home_aside_ul{overflow: hidden;width: 300px;height: 300px;margin-left: 50px; }
	.home_aside_ul li{float:left;width: 148px;height: 148px}
	.home_aside_ul_img{
		border: none;
		width: 148px;
		height: 148px;
		cursor:pointer;
		transition: all .5s ease;
		-moz-transition: all .5s ease;
		-webkit-transition: all .5s ease;	
		-o-transition: all .5s ease;
	}
	.home_aside_ul li:first-child{padding: 0 2px 2px 0}
	.home_aside_ul li:nth-child(2){padding: 0 0px 2px 2px}
	.home_aside_ul li:nth-child(3){padding: 2px 2px 0 0}
	.home_aside_ul li:nth-child(4){padding: 2px 0 0 2px}
	.home_aside_ul_img:hover{
		
		transform: rotate(360deg);
	  -ms-transform: rotate(360deg);		
	  -webkit-transform: rotate(360deg);	
	  -o-transform: rotate(360deg);		
	  -moz-transform: rotate(360deg);
	}
	*/
</style>
