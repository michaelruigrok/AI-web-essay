<template>
	<div>
		<div id="recaptcha">
			<form class="center-both" action="?" method="POST">
				<div id="captcha" class="g-recaptcha"></div>
			</form>
			<a @click.once="skipTest" tabindex="-1">{{ nope }}</a>
		</div>
	</div>
</template>

<style>

#recaptcha > form {
	margin-top: 3em;
	margin-bottom: 1.5em;
}

#recaptcha {
	position: absolute;
	left: 50%;
	transform: translateX(-50%);
}

</style>

<script>
export  default {
	name: 'ReCaptcha',
	data () {
		return {
			nope: "Skip",
		}
	},
	props: ['loadArticle'],
	methods: {
		recaptchaInit() {
			var self = this;
			setTimeout(function() {
				if(typeof grecaptcha === 'undefined') {
					self.recaptchaInit();
				} else { 
					this.captchaInstance = grecaptcha.render('captcha', {
						//sitekey: "6Lej6jUUAAAAABck65Ubc0SLrkUjzOOwtz3TyBHM", // production
						sitekey: "6LfYhTQUAAAAAIgDmbaMf_rrLkUm2ULmBOUtP9Go", // development
						callback: self.passTest,
					});
				} 
			}, 10);
		},
		skipTest() {
			var vm = this;
			setTimeout(function () {
				vm.$emit('submitted', false);
			}, 500);
		},

		passTest() {
			var vm = this;
			setTimeout(function () {
				vm.$emit('submitted', true);
			}, 800);
		},

		recaptchaCallback() {
			recaptcha.submit();
		},

		triggerClick(element) {
			var evObj = document.createEvent('Events');
			evObj.initEvent('Click', true, false);
			element.dispatchEvent(evObj);
		},
	},
	mounted: function() {
		this.recaptchaInit();
	},
	created: function() {
		$.getScript("https://www.google.com/recaptcha/api.js?render=explicit");
		return;
	}
}
</script>

