---
layout: tisseo
title: Liste des lignes perturbées.
short_title: Les lignes perturbées
next_section: 
prev_section: TisseoMessages
permalink: /projects/tisseo-api.net/TisseoLinesDisrupted/
project: TisseoAPI.Net
comments: true
description: "L'API de recherche de lieux pour Tisséo, le transport publique de la ville de Toulouse."
tags: [metro, bus, tram, Toulouse, .Net, C# ]
---

<h1><code class="option"><h1>TisseoLinesDisrupted</h1></code></h1>

Cette API permet d’obtenir la liste de toutes les lignes perturbées du réseau.


<h4>Mode d’appel et Paramètres</h4>
{% highlight c# %}
// Paramètrer l'API TisseoLines
TisseoLinesDisrupted tisseoLinesDisrupted = new TisseoLinesDisrupted()
{
	ContentFormat = "Text"
};
LinesDisruptedData linesDisruptedData = tisseoLinesDisrupted.GetMessagesData();
// Afficher les informations des pannes pour la ligne A
foreach (var ligne in linesDisruptedData.Lines)
{
	Console.WriteLine("La ligne: {0}\nLe Message: {1}",
		ligne.ShortName,
		ligne.DisturbMessage.Content);
	var key = Console.ReadKey();
	Console.WriteLine("Taper la touch Q pour quitter ou une autre touche pour afficher le message suivant.");
	if (key.Key == ConsoleKey.Q)
		break;
	Console.Clear();
}

{% endhighlight %}



<h4>Règles de gestion</h4>
<ul>
	<li>Le « scope » d’un message indique si le message concerne une ou plusieurs lignes, ou s’il s’agit d’un message général.</li>
<li>
</ul>

<div class="note info">
<h5>
</div>
