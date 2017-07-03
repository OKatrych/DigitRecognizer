# Projekt: Rozpoznanie Cyfer Napisanych Długopisem Elektrycznym
<center>Vitalij Syrotynskyi, Katrych Oleksandr</center>

##Opis zadania i zbioru danych
Zbierano dane o cyferkach ręcznie pisanych przez 44 osoby (ok. 250 od każdej osoby). Cyferki pochodzące od 30 osób użyto do treningu, a cyferki pochodzące od 14 innych użytodo testu. Cyferki zostały pisane na specjalnym urządzeniu o rozdzielczości 500 × 500, pozwalającym zapamiętaćkolejne współrzędne (x, y) długopisu w 100-milisekundowych odstępach czasowych. Po zastosowaniu skalowania i normalizacji, współrzędne (x, y) przekształcono na wartości z przedziału [0; 100].

**Opis zbioru danych**

Nazwa pliku | Liczba rekordów  | Liczba atrybutów | Opis atrybutów |
------------|------------------|------------------|----------------|
pendigits.tra (Training)|7494| 16 input+1 class attribute |16 integer[0;100] 1 class attribute [0;9]|
pendigits.tes (Testing) |3498| 16 input+1 class attribute |16 integer[0;100] 1 class attribute [0;9]|

Klasa decyzyjna | Ilość przykładów w ‘training set’|
----------------|----------------------------------|
0               |780
1               |779
2               |780
3               |719
4               |780
5               |720
6               |720
7               |778
8               |719
9               |719

Klasa decyzyjna | Ilość przykładów w ‘testing set’  |
----------------|----------------------------------|
0               |363
1               |364
2               |364
3               |336
4               |364
5               |335
6               |336
7               |364
8               |336
9               |336

##Opis algorytmu, narzędzie programistyczne

Program napisany w jeżyku : `Java 8`<br>
Stosowano **algorytmu wstecznej propagacji błędu**. Jest to podstawowy algorytm uczenia nadzorowanego wielowarstwowych jednokierunkowych sieci neuronowych. Podaje on rzepis na zmianę wag <math xmlns="http://www.w3.org/1998/Math/MathML"><msub><mi>w</mi><mrow><mi>i</mi><mi>j</mi></mrow></msub></math> dowolnych połączeń elementów przetwarzających rozmieszczonych w sąsiednich warstwach sieci. Oparty jest on na minimalizacji sumy kwadratów błędów uczenia z wykorzystaniem optymalizacyjnej metody największego
spadku.

**Algorytm uczenia**
<br>
Krok 1: Wylosuj początkowe macierze wag `W, V` i początkowe wektory odchyleń `B, C`
<br>
Krok 2: Dla każdego wektora uczącego `X`
<br>
2.1 Wyznacz wektor wyjściowej z I warstwy (ukrytej)
<math xmlns="http://www.w3.org/1998/Math/MathML"><mi>Y</mi><mo>=</mo><mi>f</mi><mo>(</mo><mi>W</mi><mo>.</mo><mi>X</mi><mo>+</mo><mi>B</mi><mo>)</mo></math>
<br>
2.2 Wyznacz wektor wyjściowej z II warstwy (wyjściowej)
<math xmlns="http://www.w3.org/1998/Math/MathML"><mi>Z</mi><mo>=</mo><mi>f</mi><mo>(</mo><mi>V</mi><mo>.</mo><mi>Y</mi><mo>+</mo><mi>C</mi><mo>)</mo></math>
<br>
2.3 Wyznacz błędy neuronów
<br>
a) Warstwa wyjściowa: 
<math xmlns="http://www.w3.org/1998/Math/MathML"><msub><mi>&#x3B4;</mi><mi>k</mi></msub><mo>=</mo><mi>f</mi><mo>&#x2019;</mo><mo>(</mo><mi>n</mi><mi>e</mi><msub><mi>t</mi><mi>k</mi></msub><mo>)</mo><mo>(</mo><msub><mi>d</mi><mi>k</mi></msub><mo>&#x2013;</mo><msub><mi>y</mi><mi>k</mi></msub><mo>)</mo><mo>(</mo><mi>d</mi><mi>l</mi><mi>a</mi><mo>&#xA0;</mo><mi>k</mi><mo>=</mo><mn>1</mn><mo>,</mo><mn>2</mn><mo>,</mo><mo>.</mo><mo>.</mo><mo>.</mo><mo>,</mo><mi>K</mi><mo>)</mo></math>
<br>
b) Warstwa ukryta:
<math xmlns="http://www.w3.org/1998/Math/MathML"><msub><mi>p</mi><mi>j</mi></msub><mo>=</mo><mi>f</mi><mo>&#x2019;</mo><mo>(</mo><mi>n</mi><mi>e</mi><msub><mi>t</mi><mi>k</mi></msub><mo>)</mo><munderover><mo>&#x2211;</mo><mrow><mi>k</mi><mo>=</mo><mn>1</mn></mrow><mi>K</mi></munderover><msub><mi>v</mi><mrow><mi>k</mi><mi>j</mi></mrow></msub><msub><mi>&#x3B4;</mi><mi>k</mi></msub><mo>&#xA0;</mo><mo>(</mo><mi>d</mi><mi>l</mi><mi>a</mi><mo>&#xA0;</mo><mi>j</mi><mo>=</mo><mn>1</mn><mo>,</mo><mn>2</mn><mo>,</mo><mo>.</mo><mo>.</mo><mo>.</mo><mo>,</mo><mi>J</mi><mo>)</mo></math>
<br>
2.2 Aktualizuj wagi `(dla i = 1,...,K)`
<br>
a) Warstwa wyjściowa:<br>
<math xmlns="http://www.w3.org/1998/Math/MathML"><msub><msup><mi>V</mi><mi>k</mi></msup><mrow><mi>n</mi><mi>e</mi><mi>w</mi></mrow></msub><mo>=</mo><mo>&#xA0;</mo><msub><msup><mi>V</mi><mi>k</mi></msup><mrow><mi>o</mi><mi>l</mi><mi>d</mi></mrow></msub><mo>+</mo><mi>&#x3B7;</mi><msub><mi>&#x3B4;</mi><mi>k</mi></msub><mi>Y</mi><mo>&#xA0;</mo><mo>(</mo><mi>d</mi><mi>l</mi><mi>a</mi><mo>&#xA0;</mo><mi>k</mi><mo>&#xA0;</mo><mo>=</mo><mo>&#xA0;</mo><mn>1</mn><mo>,</mo><mo>&#xA0;</mo><mn>2</mn><mo>,</mo><mo>&#xA0;</mo><mo>.</mo><mo>.</mo><mo>.</mo><mo>,</mo><mo>&#xA0;</mo><mi>K</mi><mo>)</mo></math>
<br>
<math xmlns="http://www.w3.org/1998/Math/MathML"><msub><msup><mi>c</mi><mi>k</mi></msup><mrow><mi>n</mi><mi>e</mi><mi>w</mi></mrow></msub><mo>=</mo><mo>&#xA0;</mo><msub><msup><mi>c</mi><mi>k</mi></msup><mrow><mi>o</mi><mi>l</mi><mi>d</mi></mrow></msub><mo>+</mo><mi>&#x3B7;</mi><msub><mi>&#x3B4;</mi><mi>k</mi></msub></math>
<br>
b) Warstwa ukryta:
<br>
<math xmlns="http://www.w3.org/1998/Math/MathML"><msub><msup><mi>W</mi><mi>j</mi></msup><mrow><mi>n</mi><mi>e</mi><mi>w</mi></mrow></msub><mo>=</mo><mo>&#xA0;</mo><msub><msup><mi>W</mi><mi>j</mi></msup><mrow><mi>o</mi><mi>l</mi><mi>d</mi></mrow></msub><mo>+</mo><mi>&#x3B7;</mi><msub><mi>p</mi><mi>j</mi></msub><mi>X</mi><mo>&#xA0;</mo><mo>(</mo><mi>d</mi><mi>l</mi><mi>a</mi><mo>&#xA0;</mo><mi>j</mi><mo>&#xA0;</mo><mo>=</mo><mo>&#xA0;</mo><mn>1</mn><mo>,</mo><mo>&#xA0;</mo><mn>2</mn><mo>,</mo><mo>&#xA0;</mo><mo>.</mo><mo>.</mo><mo>.</mo><mo>,</mo><mo>&#xA0;</mo><mi>J</mi><mo>)</mo></math>
<br>
<math xmlns="http://www.w3.org/1998/Math/MathML"><msub><msup><mi>b</mi><mi>j</mi></msup><mrow><mi>n</mi><mi>e</mi><mi>w</mi></mrow></msub><mo>=</mo><mo>&#xA0;</mo><msub><msup><mi>b</mi><mi>j</mi></msup><mrow><mi>o</mi><mi>l</mi><mi>d</mi></mrow></msub><mo>+</mo><mi>&#x3B7;</mi><msub><mi>p</mi><mi>j</mi></msub></math><br>
Krok 3: Jeśli wagi pozostały bez zmian lub `E < E min` to stop, wpp. powrót do Krok 2

Do rozwiązania problemu było stosowano trzywarstwową sieć neuronową.
![NN](img/1.png)<br>
Wagi początkowe losowane w przedziałe `[-1;1]`.<br>
Przy testowaniu sieci było obrano **współczynnik uczenia** – `0.25`.<br>
**Liczba epok** – `30`.


##Przygotowanie danych do eksperymentu

**Dane eksperymentalne**, za pomocą jeżyka `Java`, były wczytane z pliku do macierzy : `double[][]`<br>
**Dane treningowe** było podzielono na 3 części. Pierwsza polowa dla uczenia sieci. Jedna czwarta dla walidacji. Jedna czwarta dla testów uzależnionych od pisarzy. Dane testowę zostały wykorzystane do testowania sieci i oceniania jakości modelu. 


##Metoda oceniania jakości modelu

<math xmlns="http://www.w3.org/1998/Math/MathML"><mi>E</mi><mo>=</mo><mfrac><mn>1</mn><mn>2</mn></mfrac><munderover><mo>&#x2211;</mo><mrow><mi>i</mi><mo>=</mo><mn>1</mn></mrow><mi>P</mi></munderover><munderover><mo>&#x2211;</mo><mrow><mi>j</mi><mo>=</mo><mn>1</mn></mrow><mi>K</mi></munderover><mo>(</mo><msup><msub><mi>d</mi><mi>i</mi></msub><mrow><mo>(</mo><mi>j</mi><mo>)</mo></mrow></msup><mo>-</mo><msup><msub><mi>y</mi><mi>i</mi></msub><mrow><mo>(</mo><mi>j</mi><mo>)</mo></mrow></msup><msup><mo>)</mo><mn>2</mn></msup></math><br>
W końcowym wyniku udało się zdobyć **95%** poprawności sieci na danych testowych.

##Wyniki eksperymentalne
W trakcie pracy nad algorytmem najpierw było stosowano sieci dwuwarstwowej, ale wyniki testowania nie przekracały **55-65%** poprawności.  
Dalej było zaimplementowano trzywarstwową sieć i wyniku zmieniania neuronów na 1 i 2 warstwie, liczb epok i współczynnika uczenia udało się zdobyć **95%** poprawności sieci na danych testowych.  

##Algorytm wczytywania namalowanej(w naszym programie) cyfry
Przestrzeń dla rysowania `PaintArea` zrobiona za pomocą `JPanel`, nie jest bardzo fajnym narzędziem do rysowania (jeśli za szybko rysować to cyfry nie będzie widać), ale dla naszego eksperymetu tego jest wystarczająco. Został dodany nowy `MouseMotionListener` i teraz kiedy przeciskamy i poruszamy myszką to się wywoła metoda `mouseDragged(MouseEvent e)`, w niej zapisujemy pozycję myszki w wektor współrzędnych (x, y) w naszym przypadku to `ArrayList<Pair<Integer, Integer>> digitVector` i równocześnie rysujemy na wykresie. Kiedy zakończymy przesuwać myszką wywoła się metoda `mouseReleased(MouseEvent e)` w której wywołamy metodę `Tools.compressVector(digitVector)` i otrzymujemy zkompresowany vektor (8 par współrzędnych (x, y)).
##Algorytm kompresowania wektora namalowanej (w naszym programie) cyfry
Algorytm jest wykonany w metodzie `Tools.compressVector(digitVector)`. Najpierw otrzymane współrzędne (x, y) potrebno rozszerzyć tak, żeby cyfra mieściła się na krajach macierzy 100x100 (uczenie sieci wykonane na podobnych cyfrach). 
Przykład :
![Digit Progress example](img/2.png)

Następnie potrzebnym jest zmniejszenie liczby współrzędnych (x, y) do ośmiu (takie cyfry były wykorzystane dla uczenia sieci). 
Najpierw liczymy długość między wszyskimi współrzędnymi (x, y) za pomocą wzoru 
<math xmlns="http://www.w3.org/1998/Math/MathML"><mi>d</mi><mo>=</mo><msqrt><mo>(</mo><msub><mi>x</mi><mn>2</mn></msub><mo>&#x2212;</mo><msub><mi>x</mi><mn>1</mn></msub><msup><mo>)</mo><mn>2</mn></msup><mo>+</mo><mo>(</mo><msub><mi>y</mi><mn>2</mn></msub><mo>&#x2212;</mo><msub><mi>y</mi><mn>1</mn></msub><msup><mo>)</mo><mn>2</mn></msup></msqrt></math> , który został zaimplementowany w metodzie `calcDigitLength(Vector)`. Dalej dzielimy otrzymaną długość na 7 równych odcinków (7 poniważ ósmy to jest pierwzy punkt), otrzymujemy długość `X`. Szukamy 8 punktów (współrzędnych) ze długością między nimi równej `X`. 
Przykład :<br>
![Digit Progress example](img/3.png)

##Własne komentarze, wnioski. 
Oprócz samego algorytmu uczenia sieci i testowania jej na danych testowych było zaimplementowano okno dla wprowadzenia (rysowania) liczb za pomocą myszki komputerowej. Algorytm stosowany dla wybrania 16 atrybutów opisany powyżej.

