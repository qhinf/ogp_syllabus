# Schieten: nieuwe objecten maken

<!--

Projectiles schieten:
- Wie is de eigenaar van projectielen? Als de speler ze loslaat, waar blijven ze dan?
  - -> Een SpriteList in de hoofdtab
    - Kan een losse zijn, kan in de scene
  - Waar heeft de speler dan een referentie naar nodig: eigenlijk alleen die SpriteList
    - Als je de Scene doorgeeft, kun je de speler alleen gebruiken in games met een scene, terwijl je verder geen Scene functionaliteit nodig hebt
- Waar doen we collisions? -> vergelijk met enemies, dus in `on_update` in de `GameView`

Timeouts, tellen en bijhouden

Ook een dingetje: wanneer laad je textures? Voor een projectiel liever niet in de constructor, want dan moet het iedere keer opnieuw geladen worden. Dingetje is wel dat we eerst de resource handler moeten registreren... Achteraf: directe initialisatie van een field (dus gewoon `var = value` in een class) wordt maar één keer uitgevoerd, direct bij de evaluatie van de class definitie. Dus het hoeft niet per se buiten de class (al is dat misschien duidelijker). Alternatief: een aparte module waar alle textures geladen worden.

Objecten (die zichzelf) uit de game verwijderen: `remove_from_sprite_lists()`

-->