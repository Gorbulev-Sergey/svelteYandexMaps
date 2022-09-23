<script>
	// @ts-nocheck
	import { onMount } from 'svelte';
	import ComponentMap from '$lib/ComponentMap.svelte';

	let routeData = {
		// Длина маршрута
		distance: '',
		// Время прохождения маршрута
		duration: ''
	};

	function init() {
		var myMap = new ymaps.Map('map', {
			center: [55.751574, 37.573856],
			zoom: 9,
			controls: []
		});

		// Создание экземпляра маршрута.
		var multiRoute = new ymaps.multiRouter.MultiRoute(
			{
				// Точки маршрута.
				// Обязательное поле.
				referencePoints: [
					'Россия, Бабынино, улица Комсомольская, 39',
					'Россия, Калуга, улица Вилонова, 1'
				],
				// Выбор маршрута с учётом пробок
				params: {
					avoidTrafficJams: true
				}
			},
			{
				// Автоматически устанавливать границы карты так,
				// чтобы маршрут был виден целиком.
				boundsAutoApply: true
			}
		);

		// Добавление маршрута на карту.
		myMap.geoObjects.add(multiRoute);

		// Подписка на событие обновления данных маршрута.
		// Обратите внимание, подписка осуществляется для поля model.
		multiRoute.model.events.add('requestsuccess', function () {
			// Получение ссылки на активный маршрут.
			var activeRoute = multiRoute.getActiveRoute();
			// Вывод информации о маршруте.
			routeData.distance = activeRoute.properties.get('distance').text;
			routeData.duration = activeRoute.properties.get('duration').text;
			console.log('Длина: ' + activeRoute.properties.get('distance').text);
			console.log('Время прохождения: ' + activeRoute.properties.get('duration').text);
		});
	}

	onMount(() => {
		ymaps.ready(init);
	});
</script>

<ComponentMap title="Маршрут между двумя точками">
	<div slot="заголовок" class="alert alert-info small mt-3">
		<b>Информация о маршруте:</b>
		<span>длина: {routeData.distance}, время прохождения: {routeData.duration}</span>
	</div>
</ComponentMap>
