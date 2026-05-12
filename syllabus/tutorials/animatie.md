# Animatie: "bewegende" sprites

Een karakter dat altijd in dezelfde positie staat, lijkt natuurlijk een beetje raar: bij het lopen verwacht je toch bewegende benen. Gelukkig kunnen we vrij eenvoudig de texture van ons object aanpassen, om zo een animatie te maken.

## Handmatig

Je sprite kan zich in verschillende toestanden bevinden, waarvoor verschillende afbeeldingen geschikt zijn. In de constructor kun je voor iedere toestand een andere texture inladen:

```python
self.idle_texture = arcade.load_texture(":resources:pad/naar/afbeelding_idle.png")
self.jump_texture = arcade.load_texture(":resources:pad/naar/afbeelding_jump.png")
```

Voor een animatie heb je meerdere textures nodig, die je het beste in een lijst kunt inladen:

```python
self.walk_textures = [ 
    arcade.load_texture(f":resources:pad/naar/afbeelding_walk{i}.png") 
    for i in range(5)
]
```

:::{note}
Textures inladen in de constructor is prima voor objecten die één keer aangemaakt worden, maar in classes waarvan je in het spel steeds nieuwe objecten maakt, levert dat een probleem op: dezelfde afbeelding wordt dan steeds opnieuw ingeladen, waardoor de game erg langzaam kan worden. Om dat te voorkomen kun je de textures ook inladen buiten de class:

```python
TEXTURE = arcade.load_texture(":resources:pad/naar/afbeelding.png")
class Projectile(Sprite):
    # ...
```

Let er dan wel op dat je deze class dan pas importeert in *main.py* nadat de `":resources:"` handle is geregistreerd in Arcade, anders kan de afbeelding niet gevonden worden.

```python
# Maak de resources in de map resources beschikbaar als Arcade resources
arcade.resources.add_resource_handle("resources", Path(__file__).resolve().parent.parent / "resources")

# En daarna:
from projectile import Projectile
```

Een alternatief is om een speciale module te maken waarin alle textures voor de hele game geladen worden, die je dan in andere modules weer importeert.
:::

Vervolgens kun je in [`update_animation(delta_time)`](https://api.arcade.academy/en/stable/api_docs/api/sprites.html#arcade.BasicSprite.update_animation) de juiste textures aan de juiste toestand koppelen:

- Bepaal de toestand van het object, bijvoorbeeld aan de hand van positie of snelheid.
- Voor een toestand met een enkele texture, kun je die direct gebruiken:
   ```python
   self.texture = self.jump_texture
   ```
- Voor een animatie moet je bijhouden welk frame nu actief is en hoe lang dat frame al actief is: 
  ```python
  self.time_since_last_frame += delta_time
  # Als die tijd langer is dan de tijd tussen je frames
  if self.time_since_last_frame > ANIMATION_FRAME_TIME:
    # dan gaan we naar het volgende frame
    self.animation_frame = (self.animation_frame + 1) % len(self.animation_textures)
    self.texture = self.animation_textures[self.animation_frame]
    # en resetten we de timer
    self.time_since_last_frame = 0
  ```
  Eventueel kun je de frame counter en `time_since_last_frame` ook resetten bij iedere keer dat je van toestand verandert, zodat de animatie steeds bij het begin start.

Tot slot moet `update_animation` natuurlijk nog aangeroepen worden. Bij een sprite die onderdeel is van een `SpriteList`, kun je de `update_animation` methode van die lijst aanroepen op de plek waar je ook de gewone `update` methode van die lijst aanroept. Een alternatief is om `self.update_animation(delta_time)` te gebruiken in de `update` methode van je class.

## Met `TextureAnimationSprite`

Arcade heeft een aantal classes die je helpen bij het maken van geanimeerde sprites: 

- [`TextureKeyFrame`](https://api.arcade.academy/en/stable/api_docs/api/sprites.html#arcade.TextureKeyframe) koppelt een texture aan een hoeveelheid tijd dat dit frame van de animatie actief is.
- [`TextureAnimation`](https://api.arcade.academy/en/stable/api_docs/api/sprites.html#arcade.TextureAnimation) is een lijst van keyframes met een handige methode [`get_keyframe(time, loop)`](https://api.arcade.academy/en/stable/api_docs/api/sprites.html#arcade.TextureAnimation.get_keyframe) om op basis van de tijd de juiste texture op te vragen.
- [`TextureAnimationSprite`](https://api.arcade.academy/en/stable/api_docs/api/sprites.html#arcade.TextureAnimationSprite) kun je als basis voor je geanimeerde sprite gebruiken, waarbij `update_animation()` al voor je gemaakt is. Standaard werkt dit alleen voor sprites met één toestand.

Bekijk vooral [de code van `TextureAnimationSprite`](https://api.arcade.academy/en/stable/_modules/arcade/sprite/animated.html#TextureAnimationSprite) om te bepalen of het voor jouw sprite van toepassing is, of dat je het beter zelf kunt implementeren. Natuurlijk kun je dan nog steeds gebruik maken van `TextureAnimation` voor de lijst van textures.
