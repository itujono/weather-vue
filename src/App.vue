<template>
	<div id="app">
		<section class="hero is-info is-fullheight">
			<div class="hero-body">
				<div class="container">
					<img src="./assets/sun.png" width="70" alt="Sun" class="rotating-logo">
					<h1 class="title">App Cuaca buat Kamu</h1>
					<h4 class="subtitle">Dan mengapa kamu akan mencintai si iklim...</h4>
					<div class="">
						<SearchBox @addLocation="addLocation" />
						<div class="cards" v-if="cardLocations">
							<Card v-for="location in locations" :key="location.id" :location="location" @removeLocation="removeLocation" />
						</div>
						<div class="empty" v-else>
							<div class="box">
								&#9749; Masukkin aja kota mana yang pengen kamu liat cuaca nya saat ini...
							</div>
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
      locations: [],
      cardLocations: false
    };
  },
  created() {
    this.getFromLocalStorage();
  },
  methods: {
    updateLocalStorage() {
      if (window.localStorage) {
        window.localStorage.setItem(
          "weatherLocations",
          JSON.stringify(this.locations)
        );
      }
    },
    getFromLocalStorage() {
      if (
        window.localStorage &&
        window.localStorage["weatherLocations"] !== ""
      ) {
        this.locations = JSON.parse(window.localStorage["weatherLocations"]);
      }
    },
    addLocation(payload) {
      let place = {
        location: `${payload.lat}, ${payload.lon}`,
        id: payload.id
      };

      if (!this.locations.some(location => location.id === place.id)) {
        this.locations.unshift(place);
        this.updateLocalStorage();
        this.cardLocations = true;
      }

      if (this.locations.length <= 0) this.cardLocations = false;
    },
    removeLocation(id) {
      const index = this.locations.findIndex(location => location.id === id);

      this.locations.splice(index, 1);
      this.updateLocalStorage();

      if (this.locations.length <= 0) this.cardLocations = false;
    }
  }
};
</script>

<style>
#app {
	font-family: "Avenir", Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
}

.rotating-logo {
  	animation: rotator 10s infinite linear;
}

.hero-body {
  	padding-top: 0 !important;
}

.hero.is-info {
  	background-color: rgba(22, 125, 240, 0.16) !important;
}

.hero .title {
  	color: #515d80 !important;
}

.hero .subtitle {
	color: rgba(141, 164, 175, 0.9) !important;
	margin-bottom: 2.6em;
}

input.input {
  	height: 3em;
}

.container {
  	width: 800px !important;
  	max-width: 800px !important;
}

.cards {
  	margin-top: 1em;
}

.empty {
  	margin-top: 2em;
}

.empty .box {
	padding: 5rem;
	background: rgba(251, 251, 251, 0.4);
}

.slide-fade-enter-active,
.slide-fade-leave-active {
  	transition: all 0.3s ease;
}

.slide-fade-enter,
.slide-fade-leave-to {
	transform: translateY(10px);
	opacity: 0;
}

@keyframes rotator {
	from { transform: rotate(0) }
	to { transform: rotate(360deg) }
}
</style>
