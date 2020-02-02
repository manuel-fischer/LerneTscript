# Kompressionsalgorithmen

In dieser Aufgabe wird ein Konzept vorgestellt, welches nützlich ist um die Speicherung von Daten zu optimieren:
[Lauflängenkodierung](https://de.wikipedia.org/wiki/Laufl%C3%A4ngenkodierung) ist eine der einfachsten verlustfreien [Kompressionsalgorithmen](https://de.wikipedia.org/wiki/Datenkompression).
Zu einem Kompressionsalgorithmus gehören jeweils die Komprimierung und die Dekomprimierung, welche die Komprimierung rückgängig macht.

# 1. Komprimierung

Schreiben Sie eine Funktion, welches ein Array einliest und ein Array *ausspuckt*, welches aus einzelnen Anzahl-Inhalt-Paaren (Array mit zwei Elementen) besteht.

    function compress(array)

Der folgende Funktionsausruf

    compress([0, 1, 1, 1, 2, 2, 2, 2, 3, 3])
  
soll also folgendes zurückgeben

    [[1, 0], [3, 1], [4, 2], [2, 3]]

Die Funktion soll über die einzelnen Elemente laufen und zählen, wie oft ein Element nacheinander auftritt. Oben im Beispiel wird die `0` nur einmal gezählt, also wird dafür `[1, 0]` zum großen Array hinzugefügt. Die `1` wird dreimal gezählt, somit wird `[3, 1]` hinzugefügt. Usw.

---

## Tipps
<details><summary><b>Tipp 0: Zählen der Elemente</b></summary>
	
Überlegen Sie wie man hintereinander liegende gleiche Elemente zählt.

<details><summary><i>Hinweis</i></summary>
	
Optional: Schreiben Sie eine Funktion, die genau diese Aufgabe erfüllt.
Die Funktion übernimmt zwei Parameter: Das Array und die Position, ab der die wiederholenden Elemente gezählt werden sollen.

</details>
<details><summary><i>Lösung</i></summary>

Schreiben Sie das erste Element in eine Variable. Vergleichen Sie nun die folgenden Elemente im Array mit diesem, bis ein anderes Element auftritt oder das Ende des Arrays erreicht worden ist. Dabei zählen Sie mit. Diese Zahl nutzen Sie später im Anzahl-Inhalt-Paar.

</details>	
</details>

---

## Musterlösung
 
<details><summary><b>Lösung 0</b></summary>

	function adjacentCount(array, pos)
	{
		var first = array[pos];
		for var i in pos+1:array.size() do
			if array[i] != first then return i-pos;

		return array.size()-pos;
	}


	function compress(array)
	{
		var ret = [];

		var pos = 0;

		while pos != array.size() do
		{
			var count = adjacentCount(array, pos);
			ret.push([count, array[pos]]);
			pos += count;
		}

		return ret;
	}

</details>

<details><summary><b>Lösung 1</b></summary>

	function compress(array)
	{
		if array.size() == 0 then return [];
		var ret = [];
		var element = array[0];
		var count = 0;

		for var e in array do
		{
			if e == element then
			{
				count += 1;	
			}
			else
			{
				ret.push([count, element]);	

				element = e;
				count = 1;
			}
		}
		ret.push([count, element]);

		return ret;
	}

</details>


# 2. Dekomprimierung

Die Dekomprimierung ist meist einfacher als die Komprimierung, weil die Daten nicht analysiert werden muss. Schreiben Sie nun ein Programm welches den Komprimierungsvorgang rückgängig macht.

---

## Tipps

Es gibt verschiedene herangehensweisen, es ist möglich die Elemente wiederholend mit `push` zu einem Array hinzuzufügen. Jedoch gibt es auch eine weitere Möglichkeit, die hier in den Tipps behandelt wird.

<details><summary><b>Tipp 0: Array gefüllt mit einem Wert erstellen</b></summary>
	
Der Konstruktor von `Array` übernimmt 2 Parameter, die Größe des Arrays und den Inhalt, mit dem das Array gefüllt werden soll.

`Array(3, 42)` entspricht `[42, 42, 42]`
	
</details>

<details><summary><b>Tipp 1: Arrays zusammenfügen</b></summary>
	
Die Funktion `Array.concat` übernimmt zwei Arrays und gibt ein neues Array zurück, bei dem die beiden Arrays zusammengefügt sind. Diese ähnelt dem Zusammenfügen von zwei Strings mit `+`.
	
</details>

---

## Musterlösung

<details><summary><b>Lösung 0</b></summary>

	function decompress(array)
	{
		var ret = [];
		for var e in array do
			ret = Array.concat(ret, Array(e[0], e[1]));

		return ret;
	}
  
</details>

<details><summary><b>Lösung 1</b></summary>

	function decompress(array)
	{
		var ret = [];
		for var e in array do
			for 0:e[0] do
				ret.push(e[1]);

		return ret;
	}
  
</details>

