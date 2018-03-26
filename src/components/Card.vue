<template>

	<div class="box day">
		<article class="media">
			<div class="media-left">
				<h4 class="temperature">30&#176;</h4>
			</div>
			<div class="media-content">
				<div class="content">
					<div class="location">Batam </div>
					<div class="condition">Agak cerah berawan</div>
					<!-- <div class="loading"></div> -->
				</div>
			</div>
			<div class="media-right">
				<img src="" class="icon" />
				<a href="#" class="btn-remove">
					<b-icon icon="close" type="is-success"></b-icon>
				</a>
			</div>
		</article>
	</div>

</template>



<script>
	export default {
		name: "Card",
		data() {
			return {
				msg: "Welcome to Your Vue.js App"
			}
		}
	}
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

.temperature {
  font-size: 4em;
}

.location {
  font-size: 2em;
}
</style>
