---
layout: post
title: You sunk my BattleShip! [GUI with PyQt5]

---

<table>
  	<tr>
    	<th style="text-align: center; vertical-align: middle;">
    		<img src="{{ site.baseurl }}/assets/img/posts/post2/battleship_icon.png" height="110" width="170" style="border:5px solid black" align="middle">
    	</th>
    	<th>
    		<a href="https://github.com/Peter-AK/Battleship"><img src="https://gh-card.dev/repos/Peter-AK/Battleship.svg"></a>
    	</th>
  	</tr>
  	<tr>
    	<td colspan="2">
    		My take on a classic pencil and paper game with Python. The main challenges here are:
			<br>1) To create a competitive AI that can make good logical choices.
			<br>&nbsp;&nbsp; Possible look into implementation of pre-made algorithms.
			<br>2) Integrate everything with a smooth GUI/User experience using Qt for python.
			<br>&nbsp;&nbsp; I don't have much experience with GUI architecture, probably will be the most challenging part to do right.
		</td>
  	</tr>
</table>

<table>
  	<tr>
    	<td  style="background-color:#eaeaea">
			<h2> The Back-end: </h2>
			<b><br>Saturday, June 06, 2020
			<br>===============================</b>
			<p style="text-align:left;">I want this project to have a fully functional back-end before I start my work on the GUI. The idea is to have a class called Player,
			<br>this Player class will have a grid setup function that will be ran during its  __init__ method.</p>
			<p style="text-align:left;">A PC subclass will inherit Player, with an addition of random module, the Pc can setup its own ships quite easily.
			<br>(I don't think its necessary to add logic to ship placement since randomizing their locations seems like a fine strategy for me.)</p>
			<p style="text-align:left;">This is what have been implemented so far, the player and the PC can setup their ships. Initially an ANCHOR point is chosen on the gird, then a selection of the end point is made.</p>
		</td>
		<td  style="background-color:#eaeaea">
		<br>
		<br>
			<div align="middle"><img src="{{ site.baseurl }}/assets/img/posts/post2/jun-06.png"  style="border:2px solid black ">
			</div>
		</td>
  	</tr>
</table>

