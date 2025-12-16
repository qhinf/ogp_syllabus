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

## Game over

Als de speler te veel `health` heeft verloren, dan is het waarschijnlijk *game over*. Voor nu laten we gewoon het spel opnieuw beginnen, maar dat kun je later natuurlijk uitbreiden met bijvoorbeeld een bericht aan de speler of een speciaal "game over"-scherm.

Het spel wordt in eerste instantie geïnitialiseerd in de constructor van de `GameView`: alle code die daar staat zorgt ervoor dat het spel in de beginstaat wordt opgebouwd. Dat is ook wat we willen als we het spel herstarten, maar helaas kunnen we niet gewoon de constructor opnieuw uitvoeren: het object bestaat immers al, dat is de game die we spelen. Gelukkig kunnen we dit makkelijk oplossen door een nieuwe `setup` methode te maken, die we dan in de constructor ook kunnen aanroepen:

```python
class GameView(arcade.Window):
    def __init__(self, map):
        # De hoofdinitialisatie, die de grootte en titel van het scherm bepaalt
        super().__init__(constants.WINDOW_WIDTH, constants.WINDOW_HEIGHT, constants.WINDOW_TITLE)

        # Initialiseer het spel
        self.setup(map)

    def setup(self, map):
        # Hier alle andere code die eerst in __init__ stond
```

Als we het spel opnieuw starten, moeten we natuurlijk ook onthouden welke map we nu draaien, dus die slaan we op. Dan kunnen we ook een `restart` methode maken die de huidige map meegeeft om het spel te herstarten:

```python
    def setup(self, map):
        self.map = map

        # Hier alle andere code die eerst in __init__ stond

    def restart(self):
        self.setup(self.map)
```

Er zijn een heleboel manieren waarop we nu het spel opnieuw kunnen starten, maar de beste oplossing volgt een aantal regels van goed objectgeoriënteerd ontwerp. Laten we een aantal opties bekijken om die regels uit te zoeken.

### Optie: een callback

De speler kent hun eigen `health`, dus die kan ook bepalen of het *game over* is en `restart()` aanroepen. Daarvoor moet de spelere dan natuurlijk wel toegang hebben tot de game:

```python
class MainPlayer(arcade.Sprite):
    def __init__(self, game, scale = 1, center_x = 0, center_y = 0, angle = 0, **kwargs):
        super().__init__(":resources:images/characters/toon/robot/poses/character_robot_side.png", scale, center_x, center_y, angle, **kwargs)

        # Een referentie naar de game, om opnieuw te kunnen starten bij game over
        self.game = game

    def damage(self):
        self.health = self.health - 10
        # Herstart het spel als de speler dood is
        if self.health <= 0:
            self.game.restart()
```

Het nadeel hiervan is dat de speler nu toegang heeft tot alles in het spel, dus deze speler is nu heel strak aan dit spel geknoopt en kunnen we niet meer zo makkelijk in een ander spel gebruiken. We willen juist makkelijk herbruikbare onderdelen maken, dus dat is niet zo handig.

Daarnaast is het ook discutabel of het wel de verantwoordelijkheid van de speler is om het spel te herstarten. Dat is eigenlijk aan de game en niet echt aan de speler.

### Optie: controleer `health` in `on_update`

Een andere optie is dat de game zelf bepaald of het *game over* is in de `on_update` methode:

```python
class GameView(arcade.Window):
    def on_update(self, delta_time):
        # ...

        if self.player.health <= 0:
            self.restart()
```

Het nadeel hiervan is dat de game nu heel sterk afhangt van interne details van de speler: als we iets willen veranderen aan hoe de health van de speler werkt, moeten we nu zowel de `MainPlayer` als de `GameView` aanpassen. En dat terwijl het voor de game eigenlijk niet uitmaakt of we nou healthpunten gebruiken of iets heel anders doen.

### Beste optie: vraag de speler in `on_update`

We kunnen de vorige optie een klein beetje aanpassen door niet direct de `health` van de speler te pakken, maar in plaats daarvan te vragen of de speler nog in leven is.

```python
class GameView(arcade.Window):
    def on_update(self, delta_time):
        # ...

        if self.player.is_dead():
            self.restart()
```

Dan moeten we die methode natuurlijk ook aan de `MainPlayer` toevoegen:

```python
class MainPlayer(arcade.Sprite):
    def is_dead(self):
        return self.health <= 0
```

Nu is het de `GameView` die verantwoordelijk is voor het detecteren van *game over* en de bijbehorende restart in gang te zetten, maar hangt het niet af van de details hoe we de levensvatbaarheid van onze speler bepalen. We hebben nog steeds twee plekken in de code die te maken hebben met *game over*, maar die hebben duidelijk een eigen verantwoordelijkheid: als we willen aanpassen wat er gebeurt bij een *game over* of wanneer het game over is, dan moeten we in de `GameView` zijn. Willen we aanpassen wanneer een speler dood gaat, dan doen we dat in de `MainPlayer`.

Een goede vuistregel om aan te houden: in een andere class mag je alleen methoden van een class aanroepen, nooit een interne variabele van die class opvragen en al zeker niet aanpassen. Zo kun je classes goed gescheiden houden en voorkomen dat alle code aangepast moet worden als je alleen intern in de werking van een class iets wilt veranderen.

<!-- ## Power-ups: zelfde structuur als enemies, maar dan natuurlijk niet `take_damage` -->
