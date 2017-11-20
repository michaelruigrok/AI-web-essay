<template>
	<div id="app" :passed="passed">
		<navbar></navbar>
		<transition name="fade">
			<div @submitted=loadArticle :passed="passed" :is="content" id='content'></div>
		</transition>
	</div>
</template>

<script>
import Navbar from './components/Navbar';
import ReCaptcha from './components/ReCaptcha';
import MachineLearningArticle from './components/MachineLearningArticle';
//import anime from 'anime';
$.getScript("https://cdnjs.cloudflare.com/ajax/libs/animejs/2.0.2/anime.js");

export default {
	name: 'app',
	data() {
		return {
			content: ReCaptcha,
			passed: null,
		}
	},
	components: {
		Navbar,
		ReCaptcha,
		MachineLearningArticle
	},
	methods: {
		loadArticle(passed) {
			this.passed = passed;
			this.content = MachineLearningArticle;
		}
	}
}
</script>

<style>
#app, #app a {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
}

a {
	text-decoration: underline;
	cursor: pointer;
}

.center-both {
	display: flexbox;
	justify-content: center;
	height: 100%;
}

h2 {
	margin-top: 1.5rem;
}

.fade-leave-to {
	position: absolute;
	opacity: 0;
	left: 50%;
	transform: translateX(-50%);
}

.fade-enter-active, .fade-leave-active {
	transition: opacity 1.5s;
	margin-bottom: 1.5rem;
	position: absolute;
}

.fade-leave-active {
	transition: opacity 0.2s;
	left: 50%;
	transform: translateX(-50%);
}


.fade-enter {
	margin-bottom: 1.5rem;
	opacity: 0;
	position: absolute;
}
</style>
