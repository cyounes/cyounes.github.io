---
layout: tisseo
title: Liste des zones d'arrêts.
short_title: Les zones d'arrêts
next_section: TisseoStopPoints
prev_section: TisseoLines
permalink: /projects/tisseo-api.net/TisseoStopAreas/
project: TisseoAPI.Net
comments: true
description: "L'API de recherche de lieux pour Tisséo, le transport publique de la ville de Toulouse."
tags: [metro, bus, tram, Toulouse, .Net, C# ]
---

<h1><code class="option"><h1>TisseoStopAreas</h1></code></h1>

Cette API permet d’obtenir des listes de zones d’arrêts.

<h4>Mode d’appel et Paramètres</h4>
{% highlight c# %}
// Paramètrer l'API
TisseoStopAreas tisseoStopAreas = new TisseoStopAreas() 
{
	DisplayLines = true,
	DisplayCoordXY = true
};
// Récupérer les données 
StopAreasData stopAreasData = tisseoStopAreas.GetStopAreasData();

{% endhighlight %}

<h4>Règles de gestion</h4>
<ul>
<li>lineId est l’id récupéré par la requête de liste des lignes.</li>
<img src="/img/projects/tisseo/bbox.png" />
<li>Les différentes options et filtres peuvent être combinés ensemble.</li>
</ul>