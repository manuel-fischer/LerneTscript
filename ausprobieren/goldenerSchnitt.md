Folgender Code kann genutzt werden, um den [Goldenen Schnitt](https://de.wikipedia.org/wiki/Goldener_Schnitt) anzunähern

	var phi = 10; # Beliebiger Positiver Wert

	for var i in 0:20 do
	{
		phi = 1 + 1/phi;
		print(i + ": " + phi);
	}
	
Ändern Sie den Initialisierer von `phi` zu anderen Zahlen.
Sie werden merken, dass es bei einigen negativen Werten auch funktioniert.
Allerdings funktioniert es nicht bei Zahlen wie `0`, `-1`, `-0.5`, usw. nicht, weil eine Division mit 0 eintritt.

Probieren Sie aus, finden Sie weitere Zahlen, bei denen nach einiger Zeit Division mit 0 auftritt.
