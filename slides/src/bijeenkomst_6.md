# Objectgeoriënteerd Programmeren

<!-- .element: style="font-size: 2.2em;" -->

Q-highschool / Bijeenkomst 6

---

## Vandaag

- Inchecken
- Een healthbar tekenen
- Powerups plaatsen via Tiled
- Beoordeling?
- Uitchecken

***

<!-- .slide: style="text-align: left" -->

## Inchecken

Wat heb je nog gedaan?

Wat wil je vandaag leren?

***

## Verder vandaag

- Een healthbar tekenen
- Powerups plaatsen via Tiled
- Beoordeling?

Notes:
- Een healthbar: `arcade.draw_rectangle_filled`
  - Is dat een Sprite? Nee, het is niet een gameobject waar je mee interacteert
  - Dus direct in `draw` tekenen, of als een zelfstandig object; evt door het object zelf laten tekenen als het mee moet bewegen
- Power ups: vergelijkbaar met enemies, projectielen
  - Geen `take_damage`, maar ...
  - Plaatsen via Tiled, in een aparte laag en dan `layer_options = { "PowerUp": { "custom_class": PowerUp } }`, zie [TileMap docs](https://api.arcade.academy/en/latest/api_docs/api/tilemap.html)
- Wat doen we voor de beoordeling? Een gesprek? Een verslagje? Een kleine presentatie (alleen voor mij)?
  - Gebruik GitHub om te laten zien wat je hebt gedaan! In commits, in PRs, de git graph...

***

<!-- .slide: style="text-align: right" -->

## Uitchecken

Wat heb je vandaag geleerd?

Wat wil je voor de volgende bijeenkomst zelf doen?

Wat wil je in de volgende bijeenkomst leren?
