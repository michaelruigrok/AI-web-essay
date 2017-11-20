<template>
	<div>
		<div id="training">
			<h4>Training</h4>
			<p>Sample input: {{ random }}</p>
			<button @click="biggerThan" type="button">Higher than range</button>
			<button @click="inRange" type="button">Within the Range</button>
			<button @click="lowerThan" type="button">Lower than range</button>
			<br/>
			<button @click="reset" type="button">Start Over</button>
		</div>
		<form id="algorithm" @submit="algorithm" onsubmit="return false" >
			<input size="4" maxlength=4 v-model="inputNum"/>
			<input value="Run" type="submit"/>
			<p>{{ outputNum }}</p>
		</form>
		<p class="split1-test svg-text">Machine defined test</p>
		<p class="split2-test svg-text">Machine defined test</p>

		<p class="result-top svg-text">Within the Range</p>
		<p class="result-middle svg-text">Higher than Range</p>
		<p class="result-bottom svg-text">Lower than Range</p>

		<svg xmlns="http://www.w3.org/2000/svg" width="80%" viewBox="0 0 200 100">
			<!-- bottom path -->
			<path d="M 40 50 L 80 50, 80 75, 170 75" fill="none"/>
			<!-- middle path -->
			<path d="M 40 50 L 80 50 80 30 110 30, 110 45, 170 45" fill="none"  />
			<!-- top path -->
			<path d="M 40 50 L 80 50, 80 30, 110 30, 110 15, 170 15" fill="none"  />

			<!-- same, but to be highlighted when form filled in -->
			<path :visibility="highlight[0]" class="highlighted" d="M 40 50 L 80 50, 80 75, 170 75" fill="none"/>
			<path :visibility="highlight[1]" class="highlighted" d="M 40 50 L 80 50 80 30 110 30, 110 45, 170 45" fill="none"  />
			<path :visibility="highlight[2]" class="highlighted" d="M 40 50 L 80 50, 80 30, 110 30, 110 15, 170 15" fill="none"  />

			<!-- Old lines that I don't have the heart to remove :( -->
			<!-- starting line -->
			<line x1="20%" y1="50%" x2="40%" y2="50%" stroke-width="1" class="horizontal"/>

			<!-- first split -->
			<line x1="40%" y1="30%" x2="40%" y2="75%" stroke-width="1" class="vertical"/>
			<line x1="40%" y1="30%" x2="55%" y2="30%" stroke-width="1" class="horizontal"/>
			<line x1="40%" y1="75%" x2="85%" y2="75%" stroke-width="1" class="horizontal"/>

			<!-- second split -->
			<line x1="55%" y1="15%" x2="55%" y2="45%" stroke-width="1" class="vertical"/>
			<line x1="55%" y1="15%" x2="85%" y2="15%" stroke-width="1" class="horizontal"/>
			<line x1="55%" y1="45%" x2="65%" y2="45%" stroke-width="1" class="horizontal"/>

			<!-- merge bottom two -->
			<line x1="65%" y1="45%" x2="65%" y2="60%" stroke-width="1" class="vertical"/>
			<line x1="65%" y1="60%" x2="67%" y2="60%" stroke-width="1" class="horizontal"/>
			<line x1="67%" y1="60%" x2="67%" y2="75%" stroke-width="1" class="vertical"/>
		</svg>
	</div>
</template>

<script>
var MIN, MAX, belowRange, aboveRange, lowRange, highRange;
init();

function init() {
	MIN = 0;
	MAX = 1000;
	belowRange = MIN;
	aboveRange = MAX;
	lowRange = getAvg(MIN, MAX);
	highRange = lowRange;
}

function getAvg(num1, num2) {
return Math.floor((num1 + num2) / 2)
}

export default {
	name: 'AlgorithmExample',
	data () {
		return {
			height: window.screen.availHeight,
			inputNum: "",
			num: 0,
			outputNum: "",
			highlight: ["hidden", "hidden", "hidden"],
			random: this.generateNumber(),
		}
	},
	methods: {
		reset() {
			init();
			this.generateNumber();
		},
		animatePath(pathNum, hiddenArray) {
			anime({
				targets: '.highlighted',
				strokeDashoffset: [anime.setDashoffset, 0],
				easing: 'easeInSine',
				duration: 1200,
				loop: false,
				complete: function() { hiddenArray[pathNum - 1] = "hidden"; }
			});
		},
		generateNumber() {
			var method = Math.random();
			if (method < 0.15) {
				//15% of the time, return a number that's in between highRange and aboveRange
				var maxRange = aboveRange - highRange;
				this.random = Math.floor((Math.random() * maxRange) + highRange)
			} else if (method < 0.3) {
				//15% of the time, return a number that's in between belowRange and lowRange
					var maxRange = lowRange - belowRange;
					this.random = Math.floor((Math.random() * maxRange) + belowRange + 1)

			} else if (method < 0.6) {
				//30% of the time, return a number that's in between aboveRange and belowRange
				var maxRange = aboveRange - belowRange;
				this.random = Math.floor((Math.random() * maxRange) + belowRange + 1)
			} else {
				// 40% of the time, pick a completely random number
				this.random = Math.floor(Math.random() * (MAX  - MIN) + MIN - 1)
			}
			console.log('\n',belowRange, lowRange, highRange, aboveRange, maxRange, this.random);

			if (isNaN(this.random)) {
				init();
			}

			return this.random;
		},
		lowerThan() {
			var rand = this.random;
			if (belowRange < rand) {
				belowRange = rand;

				if (lowRange <= rand) {
					if (lowRange >= highRange) {
						// lowRange == highRange when initialised.
						// lowRange should never go above highRange, so I'm resetting it just in case
						// reset low and high Range in between the lowest and the highest
						highRange = getAvg(belowRange, aboveRange);
						lowRange = highRange;
					} else {
						// move lowRange directly in between belowRange and highRange
						lowRange = getAvg(belowRange, highRange);
					}
				}
			}
			this.generateNumber();
		},
		biggerThan() {
			var rand = this.random;
			if (aboveRange > rand) {
				aboveRange = rand;

				if (highRange >= rand) {
					if (highRange <= lowRange) {
						// lowRange == highRange when initialised.
							// lowRange should never go above highRange, so I'm resetting it just in case
						// reset low and high Range in between the lowest and the highest
						highRange = getAvg(belowRange, aboveRange);
						lowRange = highRange;
					} else {
						// move highRange directly in between aboveRange and lowRange
						highRange = getAvg(aboveRange + lowRange);
					}
				}
			}
			this.generateNumber();
		},
		inRange() {
			var rand = this.random;
			if (rand < lowRange) {
				lowRange = rand;

				if (rand < belowRange) {
					// conflicting data was entered
					belowRange = getAvg(rand, MIN);
				}
			} else if (rand > highRange) {
				highRange = rand;

				if (rand > aboveRange) {
					// conflicting data was entered
					aboveRange = getAvg(rand, MAX);
				}
			}
			this.generateNumber();
		},
		algorithm() {
			if (isNaN(this.num = parseInt(this.inputNum))) {
				// input is invalid
				this.outputNum = "'" + this.inputNum + " ' is not a number!";
			} else {
				var num = this.num;
				var pathNum = 1;
				//default operation
				this.outputNum = num;
				// limits will be estimated at getAvg(innerLimit, outerLimit)
				// to give it that machine learny feel

				// if number is higher than the lower limit
				if (num > getAvg( lowRange, belowRange)) {
					// if number is higher than the lower limit
					if (num < getAvg(highRange, aboveRange)) {
						pathNum = 3;
					} else {
						pathNum = 2;
					}
				}

				this.highlight[pathNum - 1] = "visible";
				this.animatePath(pathNum, this.highlight);
			}

		},
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.result-middle {
	left: 77.7%;
	top: 44%;
	transform: translateX(0%);
}

#algorithm {
	top: 46%;
	left: 20%;
	position: absolute;
}

#algorithm *{
	display:flex;
	justify-content: left;
	margin: auto;
}

#training {
	text-align: center;
	position: absolute;
	left: 7%;
	height: 30%;
	justify-content: center;
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
