<template>
	<div id="app">
		<section class="hero is-info is-fullheight">
			<div class="hero-body">
				<div class="container">
					<h1 class="title">App Cuaca buat Kamu</h1>
					<h4 class="subtitle">Dan mengapa kamu akan mencintai si iklim...</h4>
					<div class="">
						<SearchBox @addLocation="addLocation" />
						<div class="cards">
							<Card v-for="location in locations" :key="location.id" :location="location" @removeLocation="removeLocation" />
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
			},
			removeLocation(id) {
				const index = this.locations.findIndex(location => location.id === id)

				this.locations.splice(index, 1)
				this.updateLocalStorage()
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

	.hero.is-info {
		background-color: rgba(22, 125, 240, 0.16) !important;
	}

	.container {
		width: 800px;
		max-width: 800px
	}

	.cards {
		margin-top: 1em;
	}
</style>
