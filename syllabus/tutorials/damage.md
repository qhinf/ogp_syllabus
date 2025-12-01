# Damage

Even een korte herhaling: een class combineert een beschrijving van gedrag met bepaalde (variabele) eigenschappen. Het gedrag beschrijven we in methodes in de class, de eigenschappen worden opgeslagen in de class-variabelen die beschikbaar zijn via `self.`

Dus, hoe implementeren we damage? We gaan uit van een scenario met een `MainPlayer` die een healthbar heeft, die terugloopt bij contact met een `Enemy`. In dit voorbeeld hebben we een enkele `Enemy`, maar dat is later eenvoudig uit te breiden naar een lijst van `Enemy`'s.

Allereerst moeten we er dus voor zorgen dat we voor de speler de eigenschap `health` kunnen bijhouden. Daarvoor kunnen we in de constructor een nieuwe class-variabele toevoegen:

```python
class MainPlayer(arcade.Sprite):
    def __init__(self, scale = 1, center_x = 0, center_y = 0, angle = 0, **kwargs):
        super().__init__(":resources:player.png", scale, center_x, center_y, angle, **kwargs)
        
        # De speler begint met 100 health punten
        self.health = 100
```

De speler heeft ook nieuw gedrag, namelijk het oplopen van damage bij contact met een `Enemy`. Daarvoor voegen we een nieuwe methode toe:

```python
    def damage(self):
        self.health = self.health - 10
```

In dit geval verliest de speler bij elke damage 10 health punten, maar je kunt dat bijvoorbeeld ook af laten hangen van het type `Enemy` door een argument mee te geven aan deze methode.

De collisioncheck voeren we uit in de hoofdclass van de game. We gaan ervan uit dat de `MainPlayer` als `self.player` en de `Enemy` als `self.enemy` beschikbaar is. In `on_update` kunnen we dan controleren of er een collision plaatsvindt met de [`arcade.check_for_collision`](https://api.arcade.academy/en/latest/api_docs/api/sprite_list.html#arcade.check_for_collision) functie:

```python
class GameView(arcade.Window):
    def on_update(self, delta_time):
        if arcade.check_for_collision(self.player, self.enemy):
            self.player.damage()
```

We doen deze check nu in de `GameView` die het hele spel regelt, omdat het over de interactie tussen twee objecten gaat en dus niet de verantwoordelijkheid van een van die twee objecten kan zijn. Dit is vergelijkbaar met de `PhysicsEngine` die vanuit de hoofdclass alle objecten bestuurt. Als de collisionchecks ingewikkelder worden, dan is het een goed idee om hier ook een aparte class (bijvoorbeeld `DamageEngine`) voor te maken, vergelijkbaar met de `PhysicsEngine`, zodat alle logica daarvoor op een plek bewaard kan worden.

<!-- TODO: game over check? -->
