---
layout: tisseo
title: Recherche de lieux.
short_title: Recherche de lieux
next_section: TisseoLines
prev_section: 
permalink: /projects/tisseo-api.net/TisseoPlaces/
project: TisseoAPI.Net
comments: true
description: "L'API de recherche de lieux pour Tisséo, le transport publique de la ville de Toulouse."
tags: [metro, bus, tram, Toulouse, .Net, C# ]
---

<h1><code class="option"><h1>TisseoPlaces</h1></code></h1>

Cette API permet à partir d’un texte (ou d’un point X,Y) d’obtenir une liste de lieux pouvant correspondre. Les lieux retournés peuvent être des rues, des arrêts, des lieux publics ou des communes connus par le système Tisséo.
Cette API ne se contente pas de rechercher les lieux contenant exactement la chaîne de caractères transmise, mais effectue une recherche plus large intégrant des prononciations proches par exemple.
Elle peut être efficacement utilisée :
</ul>

<h4>Mode d’appel et Paramètres:</h4>
{% highlight c# %}
// Paramètrer l'API
TisseoPlaces tisseoPlaces = new TisseoPlaces() 
{ 
	// Exemple des paramètres
	Term = "Tissié", 
	DisplayBestPlace = true 
};
// Récupérer les données 
PlacesData tisseoPlacesData = tisseoPlaces.GetPlacesData();
{% endhighlight %}

<h4>Règles de gestion:</h4>
<ul>
<li>Les requêtes d’autocomplétion (paramètre Term) avec moins de 3 caractères sont interdites, tenez-en compte dans votre implémentation</li>
<li>Un des 2 paramètres term ou coordinatesXY doit être fourni. Ils doivent être utilisés de manière exclusive, dans le cas contraire c’est l’option coordinatesXY qui est prise en compte uniquement.</li>
</ul>