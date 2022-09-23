<script>
	// @ts-nocheck

	export let title = '';
	export let description = '';
</script>

<div class="d-flex justify-content-between align-items-center">
	<div class="mb-3">
		<h4 class="mb-0">{title}</h4>
		<small class="text-muted">{@html description}</small>
	</div>
	<slot name="заголовок" />
</div>
<div id="map" style="width: 100%; height:70vh" />
