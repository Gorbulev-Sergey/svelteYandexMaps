<script>
	// @ts-nocheck
	import { onMount } from 'svelte';
	import { yandexMaps, yandexRoute } from '$lib/scripts/yandexMaps';
	import ComponentMap from '$lib/ComponentMap.svelte';

	let maps;
	let data = {
		// Длина маршрута
		distance: '',
		// Время прохождения маршрута
		duration: ''
	};

	onMount(async () => {
		yandexMaps().then((m) => {
			// Инициализируем карту и получаем ссылку на неё
			maps = m;
		});
	});

	function addRoute() {
		let route = yandexRoute(
			'Россия, Бабынино, улица Комсомольская, 39',
			'Россия, городской округ Калуга, деревня Мстихино'
		);
		// Подписка на событие обновления данных маршрута.
		// Обратите внимание, подписка осуществляется для поля model.
		route.model.events.add('requestsuccess', () => {
			// Получение ссылки на активный маршрут и вывод информации о маршруте.
			data = {
				distance: route.getActiveRoute().properties.get('distance').text,
				duration: route.getActiveRoute().properties.get('duration').text
			};
		});
		// Добавляем маршрут на карту
		maps.geoObjects.add(route);
	}
</script>

<ComponentMap
	title="Маршрут между двумя точками"
	description="<a href='https://yandex.ru/dev/maps/jsapi/doc/2.1/dg/concepts/router/multiRouter.html#multiRouter__get-active-route' target='blank'>cсылка на учебник<a/>"
>
	<div slot="заголовок" class="alert alert-info small mt-3">
		<b>Информация о маршруте:</b>
		<span>длина: {data.distance}, время прохождения: {data.duration}</span>
		<button class="btn btn-dark btn-sm" on:click={() => addRoute()}>Добавить маршрут</button>
	</div>
</ComponentMap>
