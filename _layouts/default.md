<!DOCTYPE html>

<html>
	<head>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, initial-scale=1">

		{% seo %}
		{% feed_meta %}

		<link rel="stylesheet" href="//fonts.googleapis.com/css?family=Merriweather:400,400italic,700,700italic|Open+Sans:400,400italic,600,600italic,700,700italic|Inconsolata:400,700">
		<link rel="stylesheet" href="{{ site.baseurl }}/css/main.css">
		<link rel="apple-touch-icon" href="{{ site.baseurl }}/apple-touch-icon.png">
		<link rel="icon" type="image/png" href="{{ site.baseurl }}/touch-icon.png" sizes="192x192">
		<link rel="icon" type="image/png" href="{{ site.baseurl }}/images/favicon.png">
		<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>


		{% if jekyll.environment == 'production' and site.google_analytics_key != '' %}
			<script>
				window.ga=window.ga||function(){(ga.q=ga.q||[]).push(arguments)};ga.l=+new Date;
				ga('create', '{{ site.google_analytics_key }}', 'auto');
				ga('send', 'pageview');
			</script>
			<script async src='https://www.google-analytics.com/analytics.js'></script>
		{% endif %}
	</head>

	<body>
		<header>
			<h1>
				<a href="{{ site.baseurl }}/"><img src="{{ site.baseurl }}/images/emblem.svg" width="40" height="40" alt="{{ site.title }} logo"></a>
				{{ site.title }}
				<button type="button" class="open-nav" id="open-nav"></button>
			</h1>

			<form action="{{ site.baseurl }}/search/" method="get">
				<input type="text" name="q" id="search-input" placeholder="Search" autofocus>
				<input type="submit" value="Search" style="display: none;">
			</form>

			<nav {% if site.show_full_navigation %}class="full-navigation"{% endif %}>
				<ul>
					<li class="nav-item top-level {% if page.url == '/' %}current{% endif %}">
						{% assign home = site.html_pages | where: 'url', '/' | first %}
						<a href="{{ site.baseurl }}/">{{ home.title }}</a>
					</li>
				</ul>

				<ul>
					{% assign grouped = site.docs | group_by: 'category' %}
					{% for group in grouped %}
						<li class="nav-item top-level {% if group.name == page.category %}current{% endif %}">
							{% assign items = group.items | sort: 'order' %}
							<a href="{{ site.baseurl }}{{ items.first.url }}">{{ group.name }}</a>
							<ul>
								{% for item in items %}
									<li class="nav-item {% if item.url == page.url %}current{% endif %}"><a href="{{ site.baseurl }}{{ item.url }}">{{ item.title }}</a></li>
								{% endfor %}
							</ul>
						</li>
					{% endfor %}
				</ul>

				<ul>
					<li class="nav-item top-level {% if page.url == '/about/' %}current{% endif %}">
						{% assign about = site.html_pages | where: 'url', '/about/' | first %}
						<a href="{{ site.baseurl }}/about/">{{ about.title }}</a>
					</li>
					<li class="nav-item top-level {% if page.url == '/conatct/' %}current{% endif %}">
						{% assign contact = site.html_pages | where: 'url', '/contact/' | first %}
						<a href="{{ site.baseurl }}/contact/">{{ contact.title }}</a>
					</li>
				</ul>
			</nav>
		</header>

		<section class="main">
			<div class="page-header">
				<h2>{% if page.category %}{{ page.category }}{% else %}{{ site.title }}{% endif %}</h2>
				<h3>{{ page.title }}</h3>
			</div>
			<article class="content">
				{{ content }}
			</article>
		</section>

		<script>
			document.getElementById("open-nav").addEventListener("click", function () {
				document.body.classList.toggle("nav-open");
			});
		</script>
	</body>
</html>

