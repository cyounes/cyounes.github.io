---
layout: tisseo
title: Horaires à un arrêt.
short_title: Horaires à un arrêt.
next_section: TisseoMessages
prev_section: TisseoStopPoints
permalink: /projects/tisseo-api.net/TisseoDepartureBoard/
project: TisseoAPI.Net
comments: true
description: "L'API de recherche de lieux pour Tisséo, le transport publique de la ville de Toulouse."
tags: [metro, bus, tram, Toulouse, .Net, C# ]
---

<h1><code class="option"><h1>TisseoDepartureBoard</h1></code></h1>

Cette API permet d’obtenir la liste des prochains passages à un poteau d’arrêt.
<div class="note warning">
  <h5>Ne concerne que les Bus et Tramway. Aucune information ne sera retournée pour le métro ou les TAD.</h5>
</div>

Un paramètre permet de préciser si l’on souhaite obtenir les horaires théoriques de la fiche horaires ou des horaires « temps réel » c'est-à-dire re-estimés en fonction des conditions de trafic.Lorsque le choix d’horaires temps réel a été fait, la réponse précise pour chaque horaire si il a pu être re- estimé <code>RealTime=true</code> ou si l’horaire reste celui indicatif de la fiche horaire <code>RealTime=false</code>.

<h4>Mode d’appel et Paramètres</h4>
{% highlight c# %}
// Paramètrer l'API TisseoLines
// L'arret Tissie: OperatorCode = 941, stopPointId=1970324837184875
TisseoDepartureBoard tisseoDepartureBoard = 
	new TisseoDepartureBoard(941, 1970324837184875, "None") 
	{ 
		DisplayRealTime = true 
	};
DepartureBoardData departureBoardData = tisseoDepartureBoard.GetDepartureBoardData();
// Afficher les horaires des prochains départs pour l'arrêt tissié
foreach (var dep in departureBoardData.Departures)
{
	Console.WriteLine("Time: {0}\nTemps RĂŠel: {1}\n\nDestinations: ",
		dep.DateTime.ToString("dd/MM/yyyy hh:mm"),
        dep.RealTime ? "OUI" : "NON");
    foreach (var des in dep.Destinations)
    {
    	Console.WriteLine(des.Name + " | " + des.CityName);
    }
    Console.WriteLine("Taper la touch Q pour quitter ou une autre touche pour afficher le message suivant.");
    var key = Console.ReadKey();
    if (key.Key == ConsoleKey.Q)
    	break;
    Console.Clear();
}
{% endhighlight %}



<h4>Règles de gestion</h4>
<ul>
	<li>Le code operateur correspond au N° de l’arrêt (poteau d’arrêt) indiqué par l’opérateur. Si il est fourni, l’opérateur de transport (network doit l’être également)</li><li>Un des 2 paramètres operatorCode (et network) ou stopPointId doit être fourni.</li>
</ul>

<div class="note info">
<h5>A noter que le contenu de la ligne présente ici est un peu différent du format dans les autres cas, c'est-à-dire des données telles que le mode de transport et l’id de la ligne ne sont pas présentes.</h5>
</div>


