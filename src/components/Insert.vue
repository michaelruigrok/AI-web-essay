<template>
	<div class="jumbotron" :height="height / 2">
		<div :is="child"></div>
	</div>
</template>

<script>
export default {
	name: 'Insert',
	props: ['child'],
	data () {
		return {
			height: window.screen.availHeight,
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
	font-weight: normal;
}

@media (min-width: 576px) {
	.jumbotron {
		padding: 5% 3% 5% 3%;
		text-align: left;
		position: relative;
	}
}

line {
	stroke: #2c3e50;
}
</style>
