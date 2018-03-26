<template>
	<div id="app">
		<section class="hero is-info is-fullheight">
			<div class="hero-body">
				<div class="container">
					<h1 class="title">App Cuaca Kamu</h1>
					<h4 class="subtitle">Dan mengapa kamu akan mencintainya...</h4>
					<div class="box">
						<SearchBox @addLocation="addLocation" />
						<div class="cards">
							<Card v-for="location in locations" :key="location.id" />
						</div>
					</div>
				</div>
			</div>
		</section>
	</div>
</template>

<script>
	import Card from "./components/Card";
	import SearchBox from "./components/SearchBox";

	export default {
		name: "App",
		components: { Card, SearchBox },
		data() {
			return {
				locations: []
			}
		},
		created() {
			this.getFromLocalStorage()
		},
		methods: {
			updateLocalStorage() {
				if (window.localStorage) {
					window.localStorage.setItem("weatherLocations", JSON.stringify(this.locations))
				}
			},
			getFromLocalStorage() {
				if (window.localStorage && window.localStorage["weatherLocations"] !== '') {
					this.locations = JSON.parse(window.localStorage["weatherLocations"])
				}
			},
			addLocation(payload) {
				let place = {
					location: `${payload.lat}, ${payload.lon}`,
					id: payload.id
				}

				if (!this.locations.some(location => location.id === place.id)) {
					this.locations.unshift(place)
					this.updateLocalStorage()
				}
			}
		}
	}
</script>

<style>
	#app {
		font-family: "Avenir", Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
	}

	.container {
		width: 800px;
		max-width: 800px
	}

	.cards {
		margin-top: 1em;
	}
</style>
