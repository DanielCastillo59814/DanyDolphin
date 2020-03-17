<script>
	import Header from './shared/Header.svelte';
	import { onMount, afterUpdate } from 'svelte';

	export let sections = [];
	function getSections() {
		sections = document.querySelectorAll('.sideline__section');
	}
	onMount(getSections);
	afterUpdate(getSections);
</script>

<style>
	h1 {
		margin-top: 0;
		margin-bottom: 50px
	}
	div.sideline__section {
		min-height: 200vh;
		text-align: center
	}
</style>

<main>
	<Header {sections}/>
	<div class="sideline__section" data-title="dany.dolphin">
		<h1>dany.dolphin</h1>
	</div>
	<div class="sideline__section" data-title="dany.dolphin">
		<h1>dany.dolphin</h1>
	</div>
	<div class="sideline__section" data-title="dany.dolphin">
		<h1>dany.dolphin</h1>
	</div>
	<div class="sideline__section" data-title="dany.dolphin">
		<h1>dany.dolphin</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
		<h1>REYENO</h1>
	</div>
	<div class="sideline__section" data-title="dany.dolphin">
		<h1>dany.dolphin</h1>
	</div>
	<div class="sideline__section" data-title="dany.dolphin">
		<h1>dany.dolphin</h1>
	</div>
</main>