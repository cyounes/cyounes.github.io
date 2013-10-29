---
layout: projects
title: Tisséo API pour Framework .Net
next_section: jmbs
prev_section: 
permalink: /projects/tisseo-api.net/
project: TisseoAPI.Net
comments: true
description: ".Net API for Tisséo, the public transportation operator in the Toulouse area."
tags: [metro, bus, tram, Toulouse, .Net, C# ]
---

<img src="/img/projects/tisseo/tisseoapi.jpg" />
<div style="margin-top:10px; padding:10px;" class="info">
<a href="tisseo.fr">Tisséo</a> est le réseau de transports en commun de la ville de Toulouse et sa région.
</div>

<h2> Mode de mise en œuvre et formats:</h2>
Les API mises à disposition permettent d'interroger les données du référentiel transport de Tisséo elles sont accessibles par les objets dans le namespace  TisseoAPI.Net.Core :

<table>
<thead>
	<tr>
		<th>API</th>
		<th>Objet renvoyé</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>
		<a href="TisseoPlaces"><code class="option">&raquo; TisseoPlaces</code></a>
		</td>
		<td><code class="yel">PlacesData</code></td>
		<td><p>Recherche de lieux. <br />[ <a href="TisseoPlaces">documentation</a> ]</p></td>
	</tr> 
¡	<tr>
		<td>		
		<a href="TisseoLines"><code class="option">&raquo; TisseoLines</code></a></td>
		<td><code class="yel">LinesData</code></td>
		<td><p>Liste des lignes.<br />[ <a href="TisseoLines">documentation</a> ]</p></td>
	</tr> 
	<tr>
		<td><a href="TisseoStopAreas"><code class="option">&raquo; TisseoStopAreas</code></a></td>
		<td><code class="yel">StopAreasData</code></td>
		<td><p>Liste des zones d'arrêts.<br />[ <a href="TisseoStopAreas">documentation</a> ]</p></td>
	</tr> 
	<tr>
		<td><a href="TisseoStopPoints"><code class="option">&raquo; TisseoStopPoints</code></a></td>
		<td><code class="yel">StopPointsData</code></td>
		<td><p>Liste des poteaux d'arrêts.<br />[ <a href="TisseoStopPoints">documentation</a> ]</p></td>
	</tr> 
	<tr>
		<td><a href="TisseoDepartureBoard"><code class="option">&raquo; TisseoDepartureBoard</code></a></td>
		<td><code class="yel">DepartureBoardData</code></td>
		<td><p>Horaires à un arrêt.<br />[ <a href="TisseoDepartureBoard">documentation</a> ]</p></td>
	</tr> 
	<tr>
		<td><a href="TisseoMessages"><code class="option">&raquo; TisseoMessages</code></a></td>
		<td><code class="yel">MessagesData</code></td>
		<td><p>Liste des messages d'information.<br />[ <a href="TisseoMessages">documentation</a> ]</p></td>
	</tr> 
	<tr>
		<td><a href="TisseoLinesDisrupted"><code class="option">&raquo; TisseoLinesDisrupted</code></a></td>
		<td><code class="yel">LinesDisruptedData</code></td>
		<td><p>Liste des lignes perturbées.<br />[ <a href="TisseoLinesDisrupted">documentation</a> ]</p></td>
	</tr> 
</tbody>
</table>

<h4>Clés d'acces:</h4>
L’utilisation des API est soumise à l’utilisation d’une clé attribuée à chaque demandeur. Cette clé doit être transmise lors de chaque appel.
Pour obtenir une clé, envoyer un mail à opendata@tisseo.fr en indiquant :
<ul>
<li>vos références : nom, prénom et/ou entreprise</li>
<li>votre mail (pourra être utilisé pour communiquer des informations sur les API)</li>
<li>vos utilisations prévues (nom de projet ? objectifs ?)</li>
</ul>