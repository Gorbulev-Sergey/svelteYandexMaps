<script>
	// @ts-nocheck
	import { onMount } from 'svelte';

	let list, list2;
	let search = { first: '', second: '' };

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
	<!-- Внутри используем on:blur с задержкой, потомучто on:value слишком быстро забирает значение, яндекс не успевает прислать данные -->
	<input
		id="search"
		type="text"
		class="form-control rounded-start"
		placeholder="Что вас интересует?"
		on:blur={function () {
			setTimeout(() => {
				search.first = this.value;
			}, 1000);
		}}
	/>
	<button class="btn btn-dark" on:click={() => console.log(search)}>Получить</button>
</div>
<input
	id="search2"
	type="text"
	class="form-control mb-2"
	placeholder="Что вас интересует?"
	on:blur={function () {
		setTimeout(() => {
			search.second = this.value;
		}, 1000);
	}}
/>
