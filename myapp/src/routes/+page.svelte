<svelte:head>
  <title>Noodles - Hack Club</title>
</svelte:head>

<!-- <h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>
<p class="text-5xl font-bold text-blue-600">Just a test to see how this works! :D</p> -->

<script lang="ts">
	// this part is vibecoded because i didn't use a boilerplate
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';
	import Lenis from 'lenis';
	import title from '$lib/assets/noodles_title.png';
	import title_lg from '$lib/assets/noodles_title_crop.png';
	import wallpaper from '$lib/assets/background_reexport.png';
	import ramenbowl from '$lib/assets/ramenbowl.png';

	onMount(() => {
		// gemini says onMount is used to wait for the page to load before starting GSAP
		// becuz gsap needs to find book element in HTML
		const lenis = new Lenis();
		lenis.on('scroll', ScrollTrigger.update);
		function raf(time: number) {
			lenis.raf(time);
			requestAnimationFrame(raf);
		}
		requestAnimationFrame(raf);
		gsap.registerPlugin(ScrollTrigger);
		

		gsap.to('.scroll-title', {
			scrollTrigger: {
				trigger: '#what',
				start: 'top bottom',
				end: 'top center',
				scrub: true
			},
			opacity: 0,
			scale: 0.5,
			ease: 'none'
		});
		
		// #WHAT animations
		(ScrollTrigger.create({
			trigger: '#what',
			start: 'top center',
			end: 'bottom center',
			toggleClass: {
				targets: '#what-text',
				className: '!text-red-600'
			}
		}),
			ScrollTrigger.create({
				toggleClass: {
					targets: '#hello-text',
					className: '!text-orange-400'
				}
			}),
			gsap.to('#bowl', {
				scrollTrigger: {
					trigger: '#what',
					start: 'top bottom',
					end: 'bottom top',
					scrub: true
					// scrub makes it work when scrolling reverse too!
				},
				rotation: -90,
				ease: 'none'
			}));
		
		});
	
		// LEARN ANIMATIONS
		// (ScrollTrigger.create({
		// 	trigger: ''
		// })

</script>

<!-- using just screen makes the site janky idk -->
<div class="min-h-screen w-full overflow-hidden bg-[#FFCC90] text-center">
	<!-- #FFCC90 is a good color -->
	<div
		style="background-image: url({wallpaper})"
		class="inset-0 flex h-screen w-screen flex-col items-center justify-center bg-cover bg-center font-[Belanosima]"
	>
		<div
			class="fixed right-0 z-20 my-auto pr-4 text-center text-lg text-red-600 lg:pr-8 lg:text-2xl"
		>
			<!-- <p class="italic">Scroll:</p> -->
			<p id="hello-text">HELLO</p>
			<p id="what-text" class="text-orange-400">WHAT?</p>
			<!-- <p id="resources-text" class="text-orange-400">RESOURCES</p> -->
			<!-- <p id="bye-text" class="text-orange-400">BYE</p> -->
		</div>
		<img
			src={title_lg}
			alt="Ramen Hack title"
			class="scroll-title my-4 hidden max-h-[30vh] w-auto md:block"
		/>
		<img
			src={title}
			alt="Ramen Hack title"
			class="scroll-title my-4 block max-h-[30vh] w-auto md:hidden -mt-20 md:mt-0"
		/>
		<div class="flex flex-col items-center justify-center gap-3 lg:flex-row z-10 -mt-10 md:mt-0">
			<p class="text-lg text-red-600">make a scroll-based website or game</p>
			<!-- <button
				class="rounded-full border-2 border-red-600 px-4 py-2 text-lg text-red-600 hover:bg-red-600 hover:text-white"
				><a href="https://forms.hackclub.com/t/aPiaPUeF2Dus">• SUBMIT HERE •</a></button
			> -->
			<a
				href="https://forms.hackclub.com/t/aPiaPUeF2Dus"
				class="rounded-full border-2 border-red-600 px-4 py-2 text-lg text-red-600 hover:bg-red-600 hover:text-white"
			>
			• SUBMIT HERE •
			</a>
			<p class="text-lg text-red-600">we'll ship you + your friends noodles!!</p>
		</div>

		<!-- <div id="book">
        
    </div> -->
	</div>

	<a href="https://hackclub.com/"
		><img
			src="https://assets.hackclub.com/flag-orpheus-top.svg"
			alt="Hack Club flag that links to Hack Club website"
			class="fixed top-0 left-0"
		/></a
	>

	<!-- <img src={ramenbowl} alt="Picture of ramen bowl" class="hidden lg:block fixed -left-80 -bottom-110 scale-75 rotate-75"> -->
	<div
		id="what"
		class="pb-8 flex min-h-screen w-screen flex-col items-center justify-center gap-20 bg-[#FFCC90] sm:px-4 md:flex-row"
	>
		<div class="flex flex-col items-center justify-center bg-[#FBE4AB] h-auto w-3/4 md:w-1/2 px-12 lg:px-20 py-4 rounded-lg">
			<p class="pt-8 font-[Belanosima] text-4xl text-red-600">How does this work?</p>
			<div class="pb-4 font-[Belanosima] text-xl">
				<ol class="py-4 list-decimal list-inside">
					<li>Connect to <a class="text-red-600 no-underline hover:underline hover:decoration-dashed decoration-red-600 decoration-2" href="https://hackatime.hackclub.com/">Hackatime</a></li>
					<li>Make a <a class="text-red-600 no-underline hover:underline hover:decoration-dashed decoration-red-600 decoration-2" href="https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories">GitHub repository</a></li>
					<li>Work on your project</li>
					<li>Ship your project and submit it to <a class="text-red-600 no-underline hover:underline hover:decoration-dashed decoration-red-600 decoration-2" href="https://forms.hackclub.com/t/aPiaPUeF2Dus">this form</a></li>

				</ol>
				<p class="italic">(Shipping means that other people can see your website/play your game online!)</p>
			</div>

			<p class="font-[Belanosima] text-4xl text-red-600 pt-4">2 hours</p>
			<div class="pb-4 font-[Belanosima] text-xl">
				<p class="py-4">If you code for 2 hours, we'll ship you instant ramen noodles.</p>
			</div>

			<p class="font-[Belanosima] text-4xl text-red-600">5+ hours with friends</p>
			<div class="font-[Belanosima] text-xl">
				<p class="py-4">If you and a friend each spend 5 hours on your projects, we'll give each of you a $25 HCB grant to eat at a restaurant together. Just include your friend's Slack ID <a class="text-red-600 no-underline hover:underline hover:decoration-dashed decoration-red-600 decoration-2" href="https://hackclub.enterprise.slack.com/archives/C0159TSJVH8">(#what-is-my-slack-id)</a> when submitting!</p>
			</div>

			<p class="font-[Belanosima] text-4xl text-red-600 py-4">ENDS JUNE 18</p>
			
		</div>
		
		<img id="bowl" src={ramenbowl} alt="Tonkotsu ramen" class="h-100 w-auto rotate-75" />
	</div>

	<div
		id="resources"
		class="hidden flex min-h-screen w-screen flex-col items-center justify-center gap-20 bg-[#c95348] sm:px-4 md:flex-row"
	>
		
	</div>

	<!-- footer area -->
	<div
		id="footer"
		class="inset-0 flex h-auto min-h-[30vh] w-screen flex-col items-center justify-center bg-[#692616] bg-cover bg-center py-8 font-[Belanosima]"
	>
		<div class="flex flex-col items-center justify-center gap-3">
			<p class="text-lg text-red-600">Made with luv by Hack Club!</p>
		<p class="text-lg text-[#FBE4AB]">Questions? Send to <a href="https://hackclub.enterprise.slack.com/archives/C0BAUMWHAA0">#noodles</a> or kaylee@hackclub.com</p>
		</div>
	</div>
</div>
