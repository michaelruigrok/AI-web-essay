<template>
	<div id="algorithm-example">
		<form id="algorithm" @submit="algorithm" onsubmit="return false" >
			<input size="4" maxlength=4 v-model="inputNum"/>
			<input value="Run" type="submit"/>
			<p>{{ outputNum }}</p>
		</form>
		<p class="split1-test svg-text">Is the number bigger than zero?</p> <p class="split2-test svg-text">Can the number be wholly divided by 2?</p>

		<p class="split1-top svg-text">Yes</p>
		<p class="split1-bottom svg-text">No</p>
		<p class="split2-top svg-text">Yes</p>
		<p class="split2-bottom svg-text">No</p>
		<p class="result-top svg-text">Matches Criteria</p>
		<p class="result-bottom svg-text">Does not Match Criteria</p>

		<svg xmlns="http://www.w3.org/2000/svg" width="80%" viewBox="0 0 200 100" preserveAspectRation="xmidYmin meet">
			<!-- bottom path -->
			<path d="M 40 50 L 80 50 80 75 170 75"/>
			<!-- middle path -->
			<path d="M 40 50 L 80 50 80 30 110 30 110 45 130 45 130 60 140 60 140 75 170 75"/>
			<!-- top path -->
			<path d="M 40 50 L 80 50 80 30 110 30 110 15 170 15"/>

			<!-- same, but to be highlighted when form filled in -->
			<path :visibility="highlight[0]" class="highlighted" d="M 40 50 L 80 50 80 75 170 75"/>
			<!-- middle path -->
			<path :visibility="highlight[1]" class="highlighted" d="M 40 50 L 80 50 80 30 110 30 110 45 130 45 130 60 140 60 140 75 170 75"/>
			<!-- top path -->
			<path :visibility="highlight[2]" class="highlighted" d="M 40 50 L 80 50 80 30 110 30 110 15 170 15"/>

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
export default {
	name: 'AlgorithmExample',
	data () {
		return {
			height: window.screen.availHeight,
			inputNum: "",
			num: 0,
			outputNum: "",
			highlight: ["hidden", "hidden", "hidden"],
		}
	},
	methods: {
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
		algorithm() {
			if (isNaN(this.num = parseInt(this.inputNum))) {
				// input is invalid
				this.outputNum = "'" + this.inputNum + " ' is not a number!";
			} else {
				var num = this.num;
				var pathNum = 1;
				//default operation
				this.outputNum = num;
				if (num > 0) {
					if (num % 2 === 0) {
						pathNum = 3;
					} else {
						pathNum = 2;
					}
				}

				this.highlight[pathNum - 1] = "visible";
				this.animatePath(pathNum, this.highlight);
			}
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

svg {
	display: block;
	margin-left: 10%;
}

path, circle{
	stroke: #2c3e50;
	stroke-width: 0.5;
	fill: none;
}

#algorithm-example > form, #algorithm-example > button {
	position: absolute;
}

#algorithm {
	top: 45%;
	left: 20%;
}

#algorithm *{
	display:flex;
	justify-content: left;
	margin: auto;
}


.highlighted {
	stroke: lime;

}

.svg-text {
	text-align: center;
	vertical-align: bottom;
	position: absolute;
	transform: translateX(-50%);
}

.split1-test {
	width: 15%;
	left: 43%;
	bottom: 70%;
}

.split1-top {
	left: 44.4%;
	top: 28.5%;
}

.split1-bottom {
	left: 44.4%;
	top: 65%;
}

.split2-test {
	width: 15%;
	left: 54%;
	bottom: 83%;
}

.split2-top {
	left: 55.5%;
	top: 16%;
}

.split2-bottom {
	left: 55.5%;
	top: 41%;
}

.result-top {
	left: 77.7%;
	top: 19.3%;
	transform: translateX(0%);
}

.result-bottom {
	left: 77.7%;
	top: 68.6%;
	transform: translateX(0%);
}
</style>
