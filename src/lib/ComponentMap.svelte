<script>
	// @ts-nocheck

	export let title;
</script>

<div class="d-flex justify-content-between align-items-center">
	<h4 class="mb-3">{title}</h4>
	<slot name="заголовок" />
</div>
<div id="map" style="width: 100%; height:70vh" />
