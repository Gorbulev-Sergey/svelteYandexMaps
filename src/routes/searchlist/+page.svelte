<script>
	// @ts-nocheck
	import { onMount } from 'svelte';
	import ComponentMap from '$lib/ComponentMap.svelte';

	let list;

	onMount(async () => {
		list = new ymaps.SuggestView('search');
	});
</script>

<div class="d-flex justify-content-between align-items-center">
	<div class="mb-3">
		<h4 class="mb-0">Поиск информации в яндекс картах</h4>
		<small class="text-muted"
			><a href="https://yandex.ru/dev/maps/jsbox/2.1/suggest">Документация</a></small
		>
	</div>
</div>

<div class="input-group">
	<input
		id="search"
		type="text"
		class="form-control"
		placeholder="Что вас интересует?"
	/>
    <button class="btn btn-dark" on:click="{() => console.log(list)}">Получить</button>
</div>
