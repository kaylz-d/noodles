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
		lenis.on('scroll', ScrollTrigger.update)
		function raf(time: number) {
			lenis.raf(time);
			requestAnimationFrame(raf);
		}
		requestAnimationFrame(raf);
		gsap.registerPlugin(ScrollTrigger);

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
				},
				rotation: -90,
				ease: 'none'
			}));
	});
</script>

<!-- using just screen makes the site janky idk -->
<div class="min-h-screen w-full bg-[#FFCC90]">
	<!-- #FFCC90 is a good color -->
	<div
		style="background-image: url({wallpaper})"
		class="inset-0 flex h-screen w-screen flex-col items-center justify-center bg-cover bg-center font-[Belanosima]"
	>
		<div class="fixed right-0 my-auto pr-4 text-center text-lg text-red-500 lg:pr-8 lg:text-2xl z-10">
			<p id="hello-text">hello</p>
			<p id="what-text" class="text-orange-400">what?</p>
			<p class="text-orange-400">FAQ</p>
			<p class="text-orange-400">guides</p>
		</div>
		<img src={title_lg} alt="Ramen Hack title" class="my-4 max-h-[30vh] w-auto hidden md:block" />
		<img src={title} alt="Ramen Hack title" class="my-4 max-h-[30vh] w-auto block md:hidden" />
		<div class="flex flex-col items-center justify-center gap-3 lg:flex-row">
			<p class="text-lg text-red-500">use cool scrolling effects</p>
			<button
				class="rounded-full border-2 border-red-500 px-4 py-2 text-lg text-red-500 hover:bg-red-500 hover:text-white"
				>• SUBMIT HERE •</button
			>
			<p class="text-lg text-red-500">get a grant to buy noodles</p>
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
	<div id="what" class="sm:px-4 flex h-screen w-screen flex-col items-center justify-center bg-[#FFCC90]">
		<p class="bold py-8 font-[Belanosima] text-4xl text-red-500">How does this work?</p>
		<p class="bold py-8 font-[Belanosima] text-2xl">More stuff to come later :D</p>
		<img id="bowl" src={ramenbowl} alt="Tonkotsu ramen" class="h-100 w-auto rotate-75" />
	</div>

	<!-- footer area -->
	<div
		class="bg-[#692616] inset-0 py-8 flex min-h-1/2 h-auto w-screen flex-col items-center justify-center bg-cover bg-center font-[Belanosima]"
	>

		<div class="flex flex-col items-center justify-center gap-3">
			<p class="text-lg text-red-500">Made with luv!</p>
			<p class="text-lg text-red-500">by Hack Club</p>
		</div>

	</div>
</div>
