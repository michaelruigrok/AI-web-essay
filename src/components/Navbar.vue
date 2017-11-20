<template>
	<header class="jumbotron">
		<h1>
			You’re Unknowingly Helping Create the Future of AI <br/><small>&mdash; And Why That’s a Good Thing.</small>
		</h1>
	</header>
</template>

<script>
export default {
	name: 'Navbar',
	data () {
		return {
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
		padding: 3rem 2rem;
	}
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
</style>
