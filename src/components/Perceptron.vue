<template>
	<div>
		<div id="training">
			<h4>Training</h4>
			<p>{{ random }}</p>
			<button @click="biggerThan" type="button">Higher than range</button>
			<button @click="inRange" type="button">Within the Range</button>
			<button @click="lowerThan" type="button">Lower than range</button>
			<button @click="reset" type="button">Reset Training</button>
		</div>
		<form id="algorithm" @submit="algorithm" onsubmit="return false" >
			<input size="4" maxlength=4 v-model="inputNum"/>
			<input value="Run" type="submit"/>
			<p>{{ outputNum }}</p>
		</form>
		<div id="labels">
			<p class="split1-test svg-text">Machine defined test</p>
			<p class="split2-test svg-text">Machine defined test</p>

			<p class="result-top svg-text">Within the Range</p>
			<p class="result-middle svg-text">Higher than Range</p>
			<p class="result-bottom svg-text">Lower than Range</p>
		</div>

		<svg xmlns="http://www.w3.org/2000/svg" width="80%" viewBox="0 0 600 250">
			<g>
				<title>perceptron</title>
				<circle r="100" id="center" cy="125" cx="300" fill="#fff"/>

				<line id="top-l" y2="45" x2="100" y1="45" x1="10"/>
				<circle r="20" id="top-c" cy="45" cx="120" fill="#fff"/>
				<line stroke-width="2" id="top-r" y2="45" x2="240" y1="45" x1="140"/>

				<line id="middle-l" y2="125" x2="100" y1="125" x1="10" fill-opacity="null" stroke-opacity="null" fill="none"/>
				<circle r="20" id="top-c" cy="125" cx="120" fill="#fff"/>
				<line id="middle-r" y2="125" x2="200" y1="125" x1="140" fill-opacity="null" stroke-opacity="null" fill="none"/>

				<line id="bottom-l" y2="205" x2="100" y1="205" x1="10"/>
				<circle r="20" id="top-c" cy="205" cx="120" fill="#fff"/>
				<line id="bottom-r" y2="205" x2="240" y1="205" x1="140"/>

				<line id="p-out" y2="125" x2="590" y1="125" x1="400"/>
			</g>

		</svg>
	</div>
</template>

<script>
export default {
	name: 'AlgorithmExample',
	data () {
		return {
			height: window.screen.availHeight,
		}
	},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

line, path, circle{
	stroke: #2c3e50;
	stroke-width: 1;
	fill: none;
}

#top-r {
	stroke-width: 3;
}

#middle-l {
	stroke-width: 2;
}

#bottom-r {
	stroke-width: 0.3;
}

#p-out {
	stroke-width: 1.5;
}

.result-middle {
	left: 77.7%;
	top: 44%;
	transform: translateX(0%);
}

#algorithm {
	top: 46%;
	left: 8%;
	position: absolute;
}

#algorithm *{
	display:flex;
	justify-content: left;
	margin: auto;
}

#training {
	position: absolute;
	left: 7%;
	height: 30%;
	justify-content: center;
}

#training, #labels, #algorithm {
	display: none;

}

#training > button {
	justify-content: center;
	margin: auto;
}

.split1-test {
	width: 15%;
	left: 43%;
	bottom: 67%;
}

.split2-test {
	width: 15%;
	left: 54%;
	bottom: 80%;
}

button {
	display: block;
}

</style>
