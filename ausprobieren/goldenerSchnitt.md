Folgender Code kann genutzt werden, um den [Goldenen Schnitt](https://de.wikipedia.org/wiki/Goldener_Schnitt) anzunähern

	var phi = 10; # Beliebiger Positiver Wert

	for var i in 0:20 do
	{
		phi = 1 + 1/phi;
		print(i + ": " + phi);
	}
	
Ändern Sie den Initialisierer von `phi` zu anderen Zahlen.
Sie werden merken, dass es bei einigen negativen Werten auch funktioniert.
Allerdings funktioniert es nicht bei Zahlen wie `0`, `-1`, weil eine Division mit 0 eintritt.
Jedoch funktioniert es wenn stattessen die Fließkommazahldarstellung verwendet wird: `0.0` oder `-1.0`.
Das Ergebnis der Division ist `Infinity`, bzw. `-Infinity`. 

Probieren Sie aus, finden Sie weitere Zahlen, bei denen nach einiger Zeit Division mit 0, also `±Infinity` (oder sehr große Zahl), auftritt:
`-0.5 == -1/2, -2/3, -3/5`

Probieren Sie auch aus den Bereich von `0:20` auf zB. `0:50` zu vergößern. Sie werden erkennen, dass sich die Zahl nach einiger Zahl stabilisiert. 

Folgender Code bricht nach einiger Zeit ab, wenn der vorherige Wert derselbe ist wie der neue. Allerdings dürfte dies mathematisch nicht eintreten, da sich der neue Wert immer um kleine Bruchteile unterscheidet. Es tritt hier trotzdem ein, weil der Computer Zahlen nur mit einer bestimmten Genauigkeit abspeichert.

	var phi = 10; # Beliebiger Positiver Wert
	var lastPhi;
	var i = 0;

	do
	{	
		lastPhi = phi;
		phi = 1 + 1/phi;
		print(i + ": " + phi);
		i += 1;
	}
	while phi != lastPhi;