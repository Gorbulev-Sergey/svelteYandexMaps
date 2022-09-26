<script>
	// @ts-nocheck
	import ComponentMap from '$lib/ComponentMap.svelte';
	import { yandexMaps } from '$lib/scripts/yandexMaps';
	import { onMount } from 'svelte';

	let currentPosition = [55.76, 37.64];
	let myPlacemark, geolocation;

	onMount(async () => {
		yandexMaps().then((maps) => {
			geolocation = ymaps.geolocation;

			// Слушаем клик на карте.
			maps.events.add('click', function (e) {
				let coords = e.get('coords');

				// Если метка уже создана – просто передвигаем ее.
				if (myPlacemark) {
					myPlacemark.geometry.setCoordinates(coords);
				}
				// Если нет – создаем.
				else {
					myPlacemark = createPlacemark(coords);
					maps.geoObjects.add(myPlacemark);
					// Слушаем событие окончания перетаскивания на метке.
					myPlacemark.events.add('dragend', function () {
						getAddress(myPlacemark.geometry.getCoordinates());
					});
				}
				getAddress(coords);
			});

			// Создание метки.
			function createPlacemark(coords) {
				return new ymaps.Placemark(
					coords,
					{
						iconCaption: 'поиск...'
					},
					{
						preset: 'islands#violetDotIconWithCaption',
						draggable: true
					}
				);
			}

			// Определяем адрес по координатам (обратное геокодирование).
			function getAddress(coords) {
				myPlacemark.properties.set('iconCaption', 'поиск...');
				ymaps.geocode(coords).then(function (res) {
					var firstGeoObject = res.geoObjects.get(0);

					myPlacemark.properties.set({
						// Формируем строку с данными об объекте.
						iconCaption: [
							// Название населенного пункта или вышестоящее административно-территориальное образование.
							firstGeoObject.getLocalities().length
								? firstGeoObject.getLocalities()
								: firstGeoObject.getAdministrativeAreas(),
							// Получаем путь до топонима, если метод вернул null, запрашиваем наименование здания.
							firstGeoObject.getThoroughfare() || firstGeoObject.getPremise()
						]
							.filter(Boolean)
							.join(', '),
						// В качестве контента балуна задаем строку с адресом объекта.
						balloonContent: firstGeoObject.getAddressLine()
					});
					myPositionFrom = new Position(
						firstGeoObject.getAddressLine(),
						myPlacemark.geometry.getCoordinates()
					);
				});
			}

			// Сравним положение, вычисленное по ip пользователя и
			// положение, вычисленное средствами браузера.
			geolocation
				.get({
					provider: 'yandex',
					mapStateAutoApply: true
				})
				.then(function (result) {
					// Красным цветом пометим положение, вычисленное через ip.
					result.geoObjects.options.set('preset', 'islands#redCircleIcon');
					result.geoObjects.get(0).properties.set({
						balloonContentBody: 'Мое местоположение'
					});
					maps.geoObjects.add(result.geoObjects);
				});
		});
	});
</script>

<ComponentMap title="Тестовое приложение, проверка api яндекс карт" />
