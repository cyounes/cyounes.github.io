---
layout: tisseo
title: Liste des messages d'information.
short_title: Les messages d'information
next_section: TisseoLinesDisrupted
prev_section: TisseoDepartureBoard
permalink: /projects/tisseo-api.net/TisseoMessages/
project: TisseoAPI.Net
comments: true
description: "L'API de recherche de lieux pour Tisséo, le transport publique de la ville de Toulouse."
tags: [metro, bus, tram, Toulouse, .Net, C# ]
---

<h1><code class="option"><h1>TisseoMessages</h1></code></h1>

Cette API permet d’obtenir la liste des messages d’information trafic et d’information commerciale des réseau de transport (pour le moment Tisséo uniquement).Ces informations sont accessibles depuis la page d’accueil de tisseo.fr.Les messages d’information sont de type « trafic » (<a href="http://www.tisseo.fr/infos/reseau">déviations de lignes, modifications d'horaires</a>)ou « communication » (<a href="http://www.tisseo.fr/infos/tisseo">informations événementielles et commerciales</a>) 


<h4>Mode d’appel et Paramètres</h4>
{% highlight c# %}
// Paramètrer l'API TisseoLines
TisseoMessages tisseoMessages = new TisseoMessages() 
{
	ContentFormat = "Text",
	DisplayImportantOnly = false
};
MessagesData messagesData = tisseoMessages.GetMessagesData();
Console.WriteLine
("Les messages reçus: {0} messages\nLa date d'expiration de ces messages: {1}",
	messagesData.Messages.Count,
    messagesData.ExpirationDate.ToString("dd/MM/yyyy hh:mm")
);
Console.WriteLine("Taper la touch Q pour quitter");
foreach (Message message in messagesData.Messages)
{
	Console.WriteLine("NÂ° {0} --------------\nTitre: {1}\nMessage:{2}\nLes lignes concernées:\n",
	messagesData.Messages.IndexOf(message) + 1, message.Title, message.Content);
	foreach (Line line in message.Lines)
		Console.Write("{0} {1} ", line.ShortName, line.Equals(message.Lines.Last()) ? "" : " - ");
	Console.WriteLine("Taper la touch Q pour quitter ou une autre touche pour afficher le message suivant.");
	var key = Console.ReadKey();
	if (key.Key == ConsoleKey.Q)
		break;
	Console.Clear();
}
Console.WriteLine("Taper n'importe quelle touche pour quitter.");
Console.ReadKey();
{% endhighlight %}



<h4>Règles de gestion</h4>
<ul>
	<li>Le « scope » d’un message indique si le message concerne une ou plusieurs lignes, ou s’il s’agit d’un message général.</li><li>La valeur « importanceLevel » indique s’il s’agit d’un message « normal » ou d’un « important » (affiché en page d’accueil de www.tisseo.fr).</li>
<li>L’url pointe sur la source officielle de l’information : une page du site tisseo.fr.</li>
</ul>

<div class="note info">
<h5>Le contenu du Message.Content sera toujours encadré par des < ![CDATA[ et ]] ></h5>
</div>


