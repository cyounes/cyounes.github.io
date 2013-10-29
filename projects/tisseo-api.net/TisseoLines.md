---
layout: tisseo
title: Liste des lignes.
short_title: Les lignes
next_section: TisseoStopAreas
prev_section: TisseoPlaces
permalink: /projects/tisseo-api.net/TisseoLines/
project: TisseoAPI.Net
comments: true
description: "L'API de recherche de lieux pour Tisséo, le transport publique de la ville de Toulouse."
tags: [metro, bus, tram, Toulouse, .Net, C# ]
---

<h1><code class="option"><h1>TisseoLines</h1></code></h1>

Cette API permet d’obtenir la liste de toutes les lignes disponibles sur le réseau.

<h4>Mode d’appel et Paramètres</h4>
{% highlight c# %}
// Paramètrer l'API
TisseoLines tisseoLines = new TisseoLines() 
{
	// Exemple des paramètres
	DisplayTerminus = true,
	Network = "Tisseo"
};
// Récupérer les données renvoyés par le serveur
LinesData tisseoLinesData = tisseoLines.GetLinesData();
// Filtrer et recupérer l'objet qui represente la ligne Metro A
Line ligneMetroA = tisseoLinesData.Lines.Where(l => l.ShortName.Equals("A")).FirstOrDefault();
{% endhighlight %}


