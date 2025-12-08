# Objectgeoriënteerd Programmeren

<!-- .element: style="font-size: 2.2em;" -->

Q-highschool / Bijeenkomst 5

---

## Vandaag

- Inchecken
- Opfrissen
- Git: merging branches
- Projectielen
- Uitchecken

***

<!-- .slide: style="text-align: left" -->

## Inchecken

Wat heb je nog gedaan?

Wat wil je vandaag leren?

***

## Opfrissen

---

Wat is het verschil tussen een class en een object?

---

Wat is een subclass?

---

Wat doet de `__init__` methode?

---

Met welk woord verwijs je in Python naar het huidige object?

- `me`
- `this`
- `self`
- `my`

<!-- .element: class="mc" -->

---

Hoe heet de class die voor de meeste "gameobjecten" wordt gebruikt in Arcade?

- `Object`
- `Sprite`
- `GameObject`
- `CanvasItem`

<!-- .element: class="mc" -->

***

## Verder vandaag

- Git: merging branches
- Projectielen
- Uitchecken

Notes:
Git:
- Committen, delen van een file committen
  - evt: featurebranches
- Pull en merge
- PR maken

Projectielen:
- Wie is de eigenaar van projectielen? Als de speler ze loslaat, waar blijven ze dan?
  - -> Een SpriteList in de hoofdtab
    - Kan een losse zijn, kan in de scene
  - Waar heeft de speler dan een referentie naar nodig: eigenlijk alleen die SpriteList
    - Als je de Scene doorgeeft, kun je de speler alleen gebruiken in games met een scene, terwijl je verder geen Scene functionaliteit nodig hebt
- Waar doen we collisions? -> vergelijk met enemies, dus in `on_update` in de `GameView`

***

<!-- .slide: style="text-align: right" -->

## Uitchecken

Wat heb je vandaag geleerd?

Wat wil je voor de volgende bijeenkomst zelf doen?

Wat wil je in de volgende bijeenkomst leren?
