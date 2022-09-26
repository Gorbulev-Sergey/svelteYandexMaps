<script>
	// @ts-nocheck
	import { onMount } from 'svelte';

	let list, list2;

	onMount(async () => {
		list = new ymaps.SuggestView('search');
		list2 = new ymaps.SuggestView('search2');
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

<div class="input-group mb-2">
	<input
		id="search"
		type="text"
		class="form-control rounded-start"
		placeholder="Что вас интересует?"
	/>
	<button class="btn btn-dark" on:click={() => console.log(list)}>Получить</button>
</div>
<input id="search2" type="text" class="form-control" placeholder="Что вас интересует?" />
