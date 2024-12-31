# Svelte Auto Animate

## [@formkit/auto-animate](https://auto-animate.formkit.com/#usage-svelte) but only the flip animation

Svelte default flip animation only works with elements that are direct children of a keyed each block.
auto-animate adds flip animations to any element, but adds enter and exit transitions as well.
This package is a fork of auto animate that keeps only the flip animation, so you can use your svelte transitions with it.

## Usage

```svelte
<script>
	import { flip } from 'svelte-auto-animate';
</script>

<div use:flip>
	...
<div>
```

That's it!
