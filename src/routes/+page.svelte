<script lang="ts">
	import '../app.css';
	import { flip } from '$lib/index.js';
	import { blur, fade, fly, scale } from 'svelte/transition';

	const { data } = $props();

	const numbers = $state(data.initialNumbers);
	const transitions = { blur: blur, fly: fly, scale: scale, fade: fade };
	let selectedTransition = $state<(typeof transitions)[keyof typeof transitions]>(transitions.blur);
	let show = $state.raw(true);

	function toggle() {
		show = !show;
	}

	function addNumber() {
		numbers.splice(Math.floor(Math.random() * numbers.length), 0, Math.random());
	}

	function shuffle() {
		numbers.sort(() => Math.random() - 0.5);
	}

	function removeNumber() {
		numbers.splice(Math.floor(Math.random() * numbers.length), 1);
	}
</script>

<main class="text-2xl grid grid-rows-[auto_auto_1fr] p-8 place-content-center gap-4">
	<h1 class="text-6xl font-bold font-mono">Svelte Auto Animate</h1>
	<h2>
		<a class="link link-primary" href="https://auto-animate.formkit.com/#usage-svelte">
			@formkit/auto-animate
		</a>
		<span>but only the flip animation</span>
	</h2>
	<div class="grid gap-4">
		<section class="join join-vertical lg:join-horizontal">
			<button class="btn btn-primary join-item" onclick={addNumber}>Add number</button>
			<button class="btn btn-primary join-item" onclick={removeNumber}>Remove number</button>
			<button class="btn btn-primary join-item" onclick={shuffle}>Shuffle</button>
			<button class="btn btn-primary join-item" onclick={toggle}>Toggle</button>
			<select class="select select-primary w-full join-item" bind:value={selectedTransition}>
				{#each Object.entries(transitions) as [name, transition]}
					<option value={transition}>{name}</option>
				{/each}
			</select>
		</section>
		<section>
			<ul use:flip>
				{#if show}
					<li class="font-bold" transition:selectedTransition={{ x: 200 }}>I should not be here</li>
				{/if}
				{#each numbers as number (number)}
					<li transition:selectedTransition={{ x: 200 }}>{number}</li>
				{/each}
			</ul>
		</section>
	</div>
</main>
<footer class="absolute bottom-0 w-full p-4">
	<ul class="grid place-content-center grid-flow-col gap-4">
		<li>
			<a aria-label="NPM" href="https://www.npmjs.com/package/svelte-auto-animate">
				<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 256 256">
					<path d="M208 208h-32V80h-48v128H48V48h160z" />
				</svg>
			</a>
		</li>
		<li>
			<a aria-label="Github" href="https://github.com/Thiagolino8/svelte-auto-animate">
				<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 98 96">
					<path
						d="M49 0a49 49 0 0 0-15 96c2 0 3-1 3-2V84c-14 3-17-5-17-5-2-6-5-8-5-8-5-3 0-3 0-3 5 1 8 5 8 5 4 8 11 6 14 4 0-3 2-5 3-6-11-1-22-5-22-24 0-6 2-10 5-14-1-1-2-6 0-13 0 0 4-1 14 5a47 47 0 0 1 12-1l12 1c9-6 13-5 13-5 3 7 1 12 1 13 3 4 5 8 5 14 0 19-11 23-22 24 1 1 3 4 3 9v14c0 1 1 2 3 2A49 49 0 0 0 49 0z"
					/>
				</svg>
			</a>
		</li>
		<li>
			<a aria-label="Bluesky" href="https://bsky.app/profile/thiagolino8.bsky.social">
				<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 64 57">
					<path
						d="M14 4c7 5 15 17 18 23v16c-2 5-8 22-21 8-7-7-4-14 9-17-8 2-16 0-18-9L0 7C0-3 9 0 14 4Zm36 0c-7 5-15 17-18 23v16c2 5 8 22 21 8 7-7 4-14-9-17 8 2 16 0 18-9l2-18c0-10-9-7-14-3Z"
					/>
				</svg>
			</a>
		</li>
		<li>
			<a aria-label="LinkedIn" href="https://www.linkedin.com/in/thiago-lino-gomes-5812581bb">
				<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
					<path
						d="M5 3.5C5 4.9 3.9 6 2.5 6S0 4.9 0 3.5 1.1 1 2.5 1 5 2.1 5 3.5zM5 8H0v16h5V8zm8 0H8v16h5v-8.4c0-4.7 6-5 6 0V24h5V13.9c0-8-9-7.6-11-3.7V8z"
					/>
				</svg>
			</a>
		</li>
	</ul>
</footer>

<style>
	svg {
		width: 2rem;
		height: 2rem;
		fill: #4a5568;

		&:hover {
			fill: #718096;
		}
	}

	:root {
		overflow-x: hidden;
		overflow-y: scroll;
	}
</style>
