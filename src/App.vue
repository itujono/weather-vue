<template>
	<div id="app">
		<section class="hero is-info is-fullheight">
			<div class="hero-body">
				<div class="container">
					<h1 class="title">App Cuaca Kamu</h1>
					<h4 class="subtitle">Dan mengapa kamu akan mencintainya...</h4>
					<div class="box">
						<SearchBox />
						<div class="cards">
							<!-- <Card /> -->
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
		components: {
			Card,
			SearchBox
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
