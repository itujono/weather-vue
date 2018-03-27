<template>

<transition name="slide-fade" mode="out-in">
	<div :class='["box", place.isDay ? "day" : "night"]'>
		<article class="media">
			<div class="media-left">
				<h4 class="temperature">{{weather.temperature}}&#176;</h4>
			</div>
			<div class="media-content">
				<div class="content">
					<div class="location">{{place.name}}, {{place.country}}</div>
					<div class="condition">{{weather.condition}}</div>
					<!-- <div class="loading"></div> -->
				</div>
			</div>
			<div class="media-right">
				<img :src="weather.icon" class="weather-icon" width="80" />
			</div>
		</article>
		<a href="#" class="btn-remove" @click.prevent="$emit('removeLocation', location.id)">
			<b-icon icon="close"></b-icon>
		</a>
	</div>
</transition>


</template>



<script>
import axios from "axios";

export default {
  name: "Card",
  props: ["location"],
  data() {
    return {
      weather: {
        condition: "",
        temperature: "",
        icon: ""
      },
      place: {
        name: "",
        country: "",
        isDay: true
      }
    };
  },
  created() {
    axios
      .get("https://api.apixu.com/v1/current.json", {
        params: {
          key: "d288854f9b8f437fb22173445182503",
          q: this.location.location
        }
      })
      .then(res => {
        const { current, location } = res.data;

        this.place.name = location.name;
        this.place.country = location.country;
        this.weather.icon = current.condition.icon;
        this.weather.condition = current.condition.text;
        this.weather.temperature = current.temp_c;
        this.place.isDay = current.is_day === 1 ? true : false;
      })
      .catch(error =>
        console.log(`Error kali ini dipersembahkan oleh ${error}`)
      );
  }
};
</script>



<style scoped>
h1,
h2 {
  	font-weight: normal;
}
ul {
	list-style-type: none;
	padding: 0;
}
li {
	display: inline-block;
	margin: 0 10px;
}
a {
  	color: #42b983;
}

.box {
	background-color: #5b9eff;
	position: relative;
}

.box .media {
  	align-items: center !important;
}

.box .media-left {
	width: 160px;
	max-width: 160px;
}

.box.night {
	background-color: #222531;
	color: #eee;
}

.box:hover .btn-remove {
	display: inline-block;
	visibility: visible;
}

.temperature {
	font-size: 4em;
	text-align: center;
}

.location {
	font-size: 2em;
	line-height: 1.3;
	color: #eee;
}

.box.day .condition {
  	color: #275a73;
}

.btn-remove .icon {
	height: 2rem;
	width: 2rem;
}

.btn-remove {
	display: none;
	visibility: hidden;
	position: absolute;
	right: -10px;
	top: -10px;
	color: rgba(0, 0, 0, 0.5);
	background: #d82b2b;
	border-radius: 50%;
	box-shadow: 2px 6px 10px rgba(0, 0, 0, 0.5);
}

.btn-remove:hover {
  	color: #fff !important;
}

.slide-fade-enter-active, .slide-fade-leave-active {
  	transition: all 0.3s ease;
}

.slide-fade-enter,
.slide-fade-leave-to {
	transform: translateY(10px);
	opacity: 0;
}
</style>
