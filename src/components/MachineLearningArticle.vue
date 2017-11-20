<template>
	<div>
		<p>{{ confirmation }} Why? Because your answers are actually being used to train AI to solve it just as well as you can.</p>

		<p>ReCAPTCHA, like a lot of the internet nowadays, is a web-standard technology from Google. It’s a kind of CAPTCHA, which stands for Completely Automated Public Turing test to tell Computers and Humans Apart. I know, they’re really reaching to make that acronym work. Google advertises it as a very user-friendly version of the test. You click the checkbox, Google checks some data from your web browser, and lets you through.</p>

		<p>However, the ReCAPTCHA might not be convinced. Maybe you don’t have a Google account or a collection of Google Cookies (for example while in a private browsing mode), or maybe you clicked the button in a noticeably un-human manner. In this case, you would have been met with this:</p>

		<div class="jumbotron"><ReCaptchaExamples></ReCaptchaExamples></div>
		<p>ReCAPTCHA calls this a ‘challenge’. It presents the user with either several separate images or one image split into a grid, taken from Google Streetview, and requires you to correctly select each square depending on whether or not it contains a particular object. While some images are pre-selected and are used to determine your humanity, some aren’t even seen by a human before being sent off to the user.</p>

		<p>For these, Google collates the responses of several individuals and then feeds this crowd-sourced answer back to Google.  They can then use these answers to inform the original Street View scene. For instance, if Street View thought that a sign was a number plate, which it would then blur out for privacy reasons, it could correct the mistake so that users could read the sign. Using ReCAPTCHA, Google can process hundreds of millions of new images every week. </p>

		<p>However, using the test to crowdsource big sets of data isn’t new. Before ReCAPTCHA was bought out by Google, the original version of the program gave obscured words for the user to identify. These words would correspond to actual text from a physical book, article or document that a scan-to-text algorithm couldn’t decipher. Using this, the program managed to completely digitize the New York Times Article Archive and a large portion of Google Books’ catalogue.</p>

		<p>The difference between the two is that while the text based CAPTCHA can fill gaps in a data set, ReCAPTCHA is feeding its results into the algorithm that Google uses for object identification. With every new result that Google receives, it improves its AI’s ability to detect objects in frame, the very task that is asked of you to prove you <i>aren’t</i> an algorithm.</p>

		<p>So what does the AI do with this data? Why does it need such a large amount of it? And why is crowd-sourcing such a valuable way to get it? To answer these questions, we need to talk about machine learning and training data. </p>

		<p>Machine learning is a way of creating algorithms which categorise, validate, or rank sets of data, without a programmer having to figure out <i>how</i> the program would do it.</p>

		<p>In a traditional program, software engineers take a set of criteria describing how to rate a group, and break it down into a series of simple tests . For instance, if a programmer might write a program that determines if a number is a positive even number. The program would check if the number is bigger than zero, and then check if the number can be divided by 2. If both tests passed, the algorithm would output ‘true’, otherwise it would output ‘false’.</p>
		<insert :child="AlgorithmExample"></insert>

		<p>In machine learning, a programmer doesn’t need to come up with the relevant tests. Instead, the machine learning algorithm is supplied with a set of input data, and what the output of the algorithm would be for each. 50, 8492, 12, 88 and 6 match the criteria, but 31, 9, -48, 0 and -2283 all fail. Using these examples, the machine learning algorithm then figures out how to make an algorithm that achieves those same results.</p>

		<p>Below is a working, interactive example of a machine learning algorithm. It uses a kind of machine learning which builds an algorithm in a similar way to how a programmer normally does – it comes up with a bunch of simple tests, which split off into different paths like branches on a tree based on the outcome. Appropriately, it’s called ‘decision tree learning’.</p>

		<p>In the example, we are going to train the machine learning algorithm so that it takes in a number and checks if that number sits in between two other numbers. So, right now, pick two numbers between 1 and 1000 for our algorithm criteria. To train the algorithm, use the tool on the left of the example. For each sample input number that appears, if it’s bigger than your two chosen numbers, click ‘Higher than range’. If it’s smaller than your numbers, click ‘Lower than range’. And if it’s in between, click “Within the range”. Once you pick the correct answer, a new number will appear so you can continue training. </p>

		<p>The diagram on the right can be used to run the algorithm and see how accurately it matched your criteria. If you run it a couple of times during your training, you should see it gradually become more accurate as you give it more examples. You can reset all your training start again by clicking the ‘Start Over’ button.</p>

		<insert :child="RangeFinderExample"></insert>

		<p>So how does a machine learning algorithm convert example data into an algorithm? It does by taking all the input values examining their characteristics to see if they have anything in common. If all the inputs with the same output value share a common trait, the algorithm can turn that fact into a simple test as part of its algorithm. </p>

		<p>Think back to our positive even number example. The algorithm would look at all values which match the criteria – 50, 8492, 12, 88 and 6. It would notice that they are all positive, and add it to the tests. However, it would also look at the inputs which failed – 31, 9, -48, 0 and -2283 – and notice that 31 and 9 didn’t pass even though they are also positive. </p>

		<p>In this situation, the algorithm would have to make sure that it didn’t <i>only</i> use whether or not the number was bigger than zero as a test. It would have to find some other characteristic to also use. Since a lot of things aren’t true 100% of the time, machine learning often needs to try lots of characteristic combinations to see which get closest to the example output. Testing lots of combinations is something computers can do much faster than humans, which is why machine learning is so valuable.</p>

		<p>For our range example, we already know that the characteristic that determines if a number fits into a particular range is how big the number is. Because of this, we can tell the machine learning algorithm not to waste time looking at if a number is a multiple of 7, or how many threes it has, and instead only focus on the number’s size. Similarly, if we have strong feeling that a group of characteristics are going to have an effect on how the algorithm works, we can tell the machine learning algorithm to start looking at those characteristics first. </p>

		<p>The ability to predetermine what characteristics are going to be important comes down to how different  a criteria’s definition and the given input are. Since ‘does a number fit in a certain range?’ effectively translates to ‘is a number smaller than this number but bigger than this other number?’, we can directly compare the input (a number) with our potential criteria (another number). </p>

		<p>To make it that easy, we actually helped out the machine learning algorithm beforehand. When somebody enters a number into the input box, the computer sees it as text, just like ‘A’ or ‘&amp;’ or ‘♬’. Before we give the user input to the computer, we convert it into a computer-readable number. Converting text to numbers was a problem solved way back when computers used typewriters as a screen (yes that’s real, look it up). It makes sense that we do it, instead of having the machine learning algorithm re-invent the wheel by trial and error.</p>

		<p>Unfortunately, we don’t always have the answer on how to jump from input to criteria. We’ll use the concept of a cat as an example. The criteria for a cat is very well defined, even if you haven’t thought about it much. If an alien came to earth with the same kind of sight a human has, you could say enough about its shape, size and colour for the alien to identify it in a photo. But it’s much more difficult to identify a cat within a list of colours and brightnesses on a grid (like how images are stored on a computer). And that’s not even taking into consideration all the possible angles the cat could be positioned. Or whether or not the cat is obscured by another object or runs off the edge of the frame. Or if the lighting is the same all across its body. Or if it’s the same colour as the background. We could go on like this for a while.</p>

		<p>This is the problem Google has to overcome when it tries to identify street signs and cars in an image. Since the people at Google are a pretty smart bunch, they do have some idea about getting a computer to recognise objects in a picture, but it’s nowhere near as accurate as it needs to be. So instead they use a type of machine learning called ‘deep learning’. There’s no pre-processing of input, and they don’t suggest that the machine learning algorithm looks at some characteristics before others. They just give it the raw image data and say “Go for it”.</p>

		<p>However, if they tried to use decision tree learning like we did before, they wouldn’t have much luck. Since each decision essentially cuts the possibilities in half, it is very easy for one test to have a very significant effect on the whole outcome of the algorithm.  When processing an image, we want slight changes to only have small effects on the algorithm. Deep learning requires a different kind of machine learning that compares the many characteristics of the input more equally. For this purpose, Google turns to neural networks. </p>

		<p>Neural networks are a type of machine learning that looks and acts similarly to the network of neurons that make up the brain. Each ‘neuron’ is called a perceptron, and instead of representing a test like a split in a decision tree would, each perceptron represents a mathematical operation. It takes in several numbers, usually from other perceptrons, and combines them in some way into a single output value. In practice, the inside of a perceptron only adds all the values together, but input values can be resized in a way that can make it perform all sorts of operations. This resizing is done using a ‘weight’, which also indicates how important an input should be considered.</p>
		<insert :child="Perceptron"></insert>
		<p>Perceptrons are arranged in rows called ‘layers’, with each taking input from the previous layer of perceptrons and outputting into the next. The outputted numbers continue to propagate through each layer of the neural network, and at the very end only one number remains. The algorithm than uses the value of this number to decide what the output will be. The more layers in between, the more opportunities the neural network has to add nuance and accuracy to its algorithm.</p>

		<p>In a decision tree, each split represents cause and effect. If one test passes, test A will run. If it failed, then test B will run. This means that each test can only lead to two other tests, and once one is decided, you can’t go to the other side. In a neural network, however, the output of a perceptron can be used in any number of the next layer’s inputs, and is often fed into <i>all</i> of them. All the layers are connected in a vast web, spreading the weight of the algorithm across the whole neural network.</p>

		<p>Google can also implement a squashing function in each perceptron. If the output number is too high or too low, the squashing function pulls the number toward 0. This means no single perceptron can have too large an effect on the next layer.</p>

		<p>Both of these effects make neural networks perfect for Google’s purpose. Given that you have enough perceptrons, neural networks are blazingly more accurate than a human or even decision tree learning could be. However, they must still work within the tradeoffs. Since the neural network has to consider so many characteristics and variables, the number of perceptrons needed in a single layer is huge. Google say their neural network has over one billion connections. With such a messy, complex system, it’s safe to say knowing what goes on inside a neural network this big is absolutely impossible. You would probably need an <i>even bigger</i> neural network to even try.</p>

		<p>So, to ensure the neural network has the right idea, and thinks the criteria is the same thing that you do, there are only two options. You can add more perceptrons to neural network and pray that it becomes better, which is also expensive when you’ve already got <i>a billion</i> of them. Or you can make sure you have mountains and mountains of varied examples. And that’s where making millions of people fill in a form comes in.</p>

		<p>It all comes down to how well that criteria is defined. If you don’t have a good understanding of what your outcome should be, the machine learning algorithm won’t either. But sometimes there just isn’t a way of accurately knowing. In the ReCAPTCHA example, a sign could be just the top section with the image, or it could include the pole, as well. In these cases, it probably depends on who you ask. And by getting as many opinions from as many people as you can, you can find the answer that serves the interests of the most people.</p>

		<p>So spreading their data collection across millions of people using ReCAPTCHA is obviously a good thing for Google, but why is it a good thing for you? Well, in the case of ReCAPTCHA, it only really helps you out if you’re using a Google product. But the principle of crowd-sourcing training data applies almost universally: the more people assist with training machine learning algorithms, the better they will be.</p>

		<p>Luis von Ahn, one of the creators of ReCAPTCHA, went on to create the language learning app Duolingo. His vision was the same as when attempted to make printed books accessible to the digital world, but this time with the translation of websites. By injecting the translation into machine learning, the same crowd-sourcing approach can be used to translate the entire web more accurately. But it’s even bigger than that.</p>

		<p>Machine learning is everywhere now. It’s used to guess what posts you’ll like more on Facebook, sure. But it’s also used to decide what job offers to show you, or if you’re safe enough to have a home loan approved. These are situations when the result of the machine learning algorithm could have a powerful effect on your life, and for the most part they are locked away behind corporate doors.</p>

		<p>Getting a machine learning algorithm wrong can be a dangerous thing. And even though it’s becoming all the more ubiquitous, machine learning still in its infancy. But this means you can still get in on the ground floor. Organisation like the <a href="https://theodi.org/">Open Data Institute</a> are working hard to ensure that machine learning works for the many, and not the few. And by supporting them you can help make the future of AI a beautiful, beautiful thing.</p>
	</div>
</template>

<script>
import Insert from './Insert'
import AlgorithmExample from './AlgorithmExample'
import RangeFinderExample from './RangeFinderExample'
import ReCaptchaExamples from './ReCaptchaExamples'
import Perceptron from './Perceptron'

export default {
	name: 'MachineLearningArticle',
	components: {
		AlgorithmExample,
		RangeFinderExample,
		ReCaptchaExamples,
		Perceptron,
		Insert
	},
	props: ['passed'],
	data () {
		return {
			confirmation: null,
			AlgorithmExample: AlgorithmExample,
			RangeFinderExample: RangeFinderExample,
			ReCaptchaExamples: ReCaptchaExamples,
			Perceptron: Perceptron,
		}
	},
	methods: {
		init() {
			this.$nextTick(function() { 
				if (this.passed) {
					this.confirmation = "Congratulations, you passed! However, by proving your humanity you may have just made that test – called a 'ReCAPTCHA' – less reliable.";
				} else {
					this.confirmation = "Didn’t want to click the “I’m not a robot” button? Don’t worry, we won’t tell anyone your secret. In all seriousness, from your utter dismay at the thought of clicking that checkbox it seems like you’ve probably encountered those tests a lot. But don’t worry, the more of the tests – or 'ReCAPTCHAs' – that are completed, the faster they become obsolete. ";
				}
			});
		}

	},
	mounted: function() {
		this.init();
	}

}
</script>

<style scoped>
#content {
	margin-bottom: 1.5rem;
}

#content p {
	width: 60%;
	margin: auto;
	margin-bottom: 2rem;
	text-align: justify;
	font-size: 1.3rem;
	line-height: 2.5rem;
}

#content > .annotation > p {
	font-size: 1em;
	background-color: #E6E6E6;
	font-family: monospace;
}

</style>
