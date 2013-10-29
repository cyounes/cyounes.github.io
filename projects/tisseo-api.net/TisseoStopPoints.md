---
layout: tisseo
title: Liste des poteaux d'arrêts.
short_title: Les poteaux d'arrêts
next_section: TisseoDepartureBoard
prev_section: TisseoStopAreas
permalink: /projects/tisseo-api.net/TisseoStopPoints/
project: TisseoAPI.Net
comments: true
description: "L'API de recherche de lieux pour Tisséo, le transport publique de la ville de Toulouse."
tags: [metro, bus, tram, Toulouse, .Net, C# ]
---

<h1><code class="option"><h1>TisseoStopPoints</h1></code></h1>

Cette API permet d’obtenir des listes d’arrêts.L’ensemble des arrêts d’un réseau, d’une zone géographique, ou d’une zone d’arrêt.

<h4>Mode d’appel et Paramètres</h4>
{% highlight c# %}
// Paramètrer l'API TisseoLines
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
/********* TisseoStopPoints *************/
// Paramètrer l'API
TisseoStopPoints tisseoStopPoints = new TisseoStopPoints()
{
	DisplayCoordXY = true,
	DisplayDestinations = true,
    DisplayLines = true,
    SortByDistance = true,
    LineId = ligneMetroA.Id.Value
};
StopPointsData stopPointsData = tisseoStopPoints.GetStopPontsData();
// Afficher les arrêts de la ligne A et leur destinations
foreach (var stpPnt in stopPointsData.StopPoints)
{
	Console.WriteLine("Nom: {0}\nDestinations:", stpPnt.Name);
	foreach (var des in stpPnt.Destinations)
	{
		Console.WriteLine("\t# {0}", des.Name);
	}
    Console.WriteLine("\n\nTaper la touch Q pour quitter ou une autre touche pour afficher le message suivant.");
    var key = Console.ReadKey();
    if (key.Key == ConsoleKey.Q)
    	break;
    Console.Clear();
}
{% endhighlight %}

<h4>Règles de gestion</h4>
<ul>
<li>Le srid permet à la fois de modifier le système de coordonnées des XY des zones d’arrêts et de préciser dans quel référentiel la bbox est exprimée.</li><li>Format attendu : latitude pt A, longitude pt A, latitude point B, longitude point B, ou A et B sont positionné comme sur le schéma suivant :</li>
<img src="/img/projects/tisseo/bbox.png" />
<li>sortByDistance ne fonctionne que si une bbox est fournie</li>
<li>stopAreaId est l’id récupéré par la requête de la liste des zones d’arrêts, lorsqu’il est utilisé avec la bbox il faut s’assurer que l’id soit bien défini dans la zone géographique.</li>
<li>Les différentes options et filtres peuvent être combinés ensemble.</li>
</ul>
