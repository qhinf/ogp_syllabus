# Objectgeoriënteerd Programmeren

<!-- .element: style="font-size: 2.2em;" -->

Q-highschool / Bijeenkomst 1

***

## Vandaag

- Wat is deze module?
- Opfrisquiz Python
- Tools
- Wegwijs in de werkplaats
- Een level maken/bewerken (?)
- Uitchecken

***

## Opfrisquiz

---

<p>Hoe print je de tekst <i>Dit is leuk!</i> met Python?</p>
<ul class="mc">
    <li><code>print(Dit is leuk!)</code></li>
    <li><code>print("Dit is leuk!")</code></li>
    <li><code>print('Dit is leuk!')</code></li>
    <li><code>print "Dit is leuk!"</code></li>
</ul>

---

<p>Wat print dit programma?</p>
<pre>
    <code>
a = 12
a = 5
print(a)
    </code>
</pre>
<ul class="mc">
    <li>12</li>
    <li>5</li>
    <li>17</li>
    <li>Dat kun je niet weten</li>
</ul>

---

<p>Wat print dit programma?</p>
<pre>
    <code>
smaller = min(14, 99
bigger = max(3, 4)
print(smaller + bigger)
    </code>
</pre>
<ul class="mc">
    <li>28</li>
    <li>SyntaxError: invalid syntax</li>
    <li>102</li>
    <li>NameError: smaller is not defined</li>
</ul>

---

Wat is de output?

```python
antwoord = "nee"
if antwoord == "ja":
    print("Oke, doen we")
else:
    print("Dan niet")
print("Dikke doei!")
```

- ```plaintext
  Oke, doen we
  Dikke doei!
  ```
- ```plaintext
  Oke, doen we
  ```
- ```plaintext
  Dan niet
  Dikke doei!
  ```
- ```plaintext
  Dan niet
  ```

<!-- .element: class="mc" -->

---

Welk van deze codes print "Hallo" als de variabele `invoer` gelijk is aan "zeg hallo"?

- ```python
  if invoer = "zeg hallo":
      print("Hallo")
  ```
- ```python
  if invoer == "zeg hallo":
      print("Hallo")
  ``` 
- ```python
  if invoer = "zeg hallo":
  print("Hallo")
  ```
- ```python
  if invoer == "zeg hallo":
  print("Hallo")
  ```

<!-- .element: class="mc" -->

---

Wat is de output?

```python
while True:
    print("We stoppen niet.")
print("Gestopt.")
```

- ```plaintext
  We stoppen niet.
  Gestopt.
  ```
- ```plaintext
  Gestopt.
  ```
- ```plaintext
  We stoppen niet.
  ```
- ```plaintext
  We stoppen niet.
  We stoppen niet.
  We stoppen niet.
  We stoppen niet.
  We stoppen niet.
  We stoppen niet.
  We stoppen niet.
  We stoppen niet.
  ...
  ```

<!-- .element: class="mc" -->

---

Wat is de output?

```python
while False:
    print("We stoppen niet.")
print("Gestopt.")
```

- ```plaintext
  We stoppen niet.
  Gestopt.
  ```
- ```plaintext
  Gestopt.
  ```
- ```plaintext
  We stoppen niet.
  ```
- ```plaintext
  We stoppen niet.
  We stoppen niet.
  We stoppen niet.
  We stoppen niet.
  We stoppen niet.
  We stoppen niet.
  We stoppen niet.
  We stoppen niet.
  ...
  ```

<!-- .element: class="mc" -->

---

Wat is de output?

```python
for i in range(0, 10):
    print(i, "* 7 =", i * 7)
```

- ```plaintext
  1 * 7 = 7
  2 * 7 = 64
  ...
  10 * 7 = 70
  ```
- ```plaintext
  0 * 7 = 0
  1 * 7 = 7
  ...
  9 * 7 = 63
  ```
- ```plaintext
  0* 7 =0
  1* 7 =7
  ...
  10* 7 =7
  ```
- ```plaintext
  0 * 7 = 0
  1 * 7 = 7
  ...
  10 * 7 = 7
  ```

<!-- .element: class="mc grid" -->

---

Wat doet `def`?

- Maakt een variabele **def**initief
- **Def**inieert een functie
- **Def**inieert een variabele
- Geeft de standaard (**def**ault) keuze

<!-- .element: class="mc" -->

---

Wat staat op de plek van de blokken?

```python
# Berekent het kwadraat van een getal
def kwadraat(x):
    &block;&block;&block;&block;&block;&block; x * x
```

- `return`
- `def:`
- `return:`
- `def`

<!-- .element: class="mc" -->

---

Wat is de output?

```python
def zeghallo(naam):
    return "Hallo, " + naam + "!"

zeghallo("Pieter")
zeghallo("Jeroen")
```

- ```plaintext
  Hallo, PieterJeroen!
  ```
- ```plaintext
  
  ```
- ```plaintext
  Hallo, !
  Hallo, !
  ```
- ```plaintext
  Hallo, Pieter!
  Hallo, Jeroen!
  ```

<!-- .element: class="mc" -->

---

```python
dieren = [ "Olifant", "Vink", "Goudvis", "Leguaan", "Muis" ]
```

Wat is `dieren[2]`?

- Olifant
- Vink
- Goudvis
- Leguaan

<!-- .element: class="mc" -->

---

```python
dieren = [ "Olifant", "Vink", "Goudvis", "Leguaan", "Muis" ]
```

Hoe pak je het laatste element uit deze lijst?

- `dieren[0]`
- `dieren[-1]`
- `dieren[len(dieren)]`
- `dieren[len(dieren) - 1]`

<!-- .element: class="mc" -->

Notes:
Zowel `dieren[-1]` als `dieren[len(dieren) - 1]` zijn correct

---

Schrijf een functie die twee getallen optelt.

- ```python
  def telop a b:
      return a + b
  ```
- ```python
  def telop(a, b):
      a + b
  ```
- ```python
  def telop(a, b):
      return a + b
  ```
- ```python
  def telop a b:
      a + b
  ```
<!-- .element: class="mc" -->

***

## Tools

- [Python](https://www.python.org/downloads/)
- [Git](https://git-scm.com/install/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Tiled](https://www.mapeditor.org/)

***

## Wegwijs<br>in de werkplaats

***

<!-- .slide: style="text-align: right" -->

## Uitchecken

Wat heb je vandaag geleerd?

Wat wil je in de volgende bijeenkomst leren?

---

## Volgende week

Fysieke bijeenkomst, tot *17:00*\
Locatie volgt
