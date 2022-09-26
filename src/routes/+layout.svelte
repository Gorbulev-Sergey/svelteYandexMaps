<nav class="navbar navbar-expand-lg navbar-light bg-light shadow-sm">
	<div class="container">
		<button
			class="navbar-toggler"
			type="button"
			data-bs-toggle="collapse"
			data-bs-target="#navbarNav"
		>
			<span class="navbar-toggler-icon" />
		</button>
		<div class="collapse navbar-collapse" id="navbarNav">
			<div class="d-flex align-items-start justify-content-between w-100">
				<ul class="navbar-nav">
					<li class="nav-item">
						<a class="nav-link" href="/">Домой</a>
					</li>
					<li class="nav-item">
						<a class="nav-link" href="/distance/betweentwopoints">Между двумя точками</a>
					</li>
					<li class="nav-item">
						<a class="nav-link" href="/searchlist">Поиск данных</a>
					</li>
				</ul>
				<ul class="navbar-nav">
					<li class="nav-item">
						<a class="nav-link" href="https://developer.tech.yandex.ru/services/" target="blank"
							>Кабинет разработчика</a
						>
					</li>
				</ul>
			</div>
		</div>
	</div>
</nav>

<div class="container my-3">
	<slot />
</div>
