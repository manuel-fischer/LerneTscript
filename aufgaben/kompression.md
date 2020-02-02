# Kompressionsalgorithmen

In dieser Aufgabe wird ein Konzept vorgestellt, welches nützlich ist um die Speicherung von Daten zu optimieren:
Lauflängenkodierung ist eine der einfachsten verlustfreien Kompressionsalgorithmen.
Zu einem Kompressionsalgorithmus gehören jeweils die Komprimierung und die Dekomprimierung, welche die Komprimierung rückgängig macht.

# 1. Komprimierung

Schreiben Sie eine Funktion, welches ein Array einliest und ein Array *ausspuckt*, welches aus einzelnen Anzahl-Inhalt-Paaren (Array mit zwei Elementen) besteht.

    function compress(array);

Der folgende Funktionsausruf

    compress([0, 1, 1, 1, 2, 2, 2, 2, 3, 3])
  
soll also folgendes zurückgeben

    [[1, 0], [3, 1], [4, 2], [2, 3]]


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

Die Dekomprimierung ist meist einfacher als die Komprimierung. Schreiben Sie nun ein Programm welches den Komprimierungsvorgang rückgängig macht.

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
			for var i in 0:e[0] do
				ret.push(e[1]);

		return ret;
	}
  
</details>

