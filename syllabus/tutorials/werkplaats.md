# Aan de slag in de Werkplaats

Van je docent heb je via Teams een GitHub Classroom link gekregen. Gebruik die link om je aan te melden en doorloop de stappen om toegang te krijgen tot de repository waarin we samen aan de game gaan werken. Eenmaal in de repository zie je een groene *Clone* knop: klik daarop en kopieer de link die je ziet staan.

## git clone

Om zelf aan de game te werken, wil je een lokale kopie van alle code op jouw computer hebben. Dat doen we vanuit Visual Studio Code: open Visual Studio Code, gebruik de toetsencombinatie <kbd>Ctrl+Shift+P</kbd> om het commandovenster te openen. Geef vervolgens het commando `Git: Clone` en druk op <kbd>Enter</kbd> om dat uit te voeren. Plak vervolgens de URL van de repository, druk wederom op <kbd>Enter</kbd> en kies een map om de code op jouw computer op te slaan. Gebruik bij voorkeur een map die niet via OneDrive (of iets anders) wordt gesynchroniseerd, want dat kan soms problemen opleveren.

## Python en Arcade

Als je de repository hebt geopend in VSCode, kunnen we Arcade installeren. We gebruiken hiervoor een "virtual environment" in Python, waarmee dependencies (zoals Arcade) alleen in de map van dit project worden opgeslagen. Gebruik wederom <kbd>Ctrl+Shift+P</kbd> en voer het commando "Python: Create Environment..." uit. Kies de optie "Quick Create (venv - Create a virtual environment in workspace root)". Nu wordt Arcade geïnstalleerd in een *.venv* map in dit project.

## De game uitvoeren

Gebruik de sneltoets F5 om het spel te starten. Je kunt ook naar de "Debug" zijbalk gaan (die met het icoon van een play-knop met een kever erbij) en vervolgens de groene play-knop bovenin het scherm gebruiken.

## Wijzigingen maken

Voordat je dingen gaat aanpassen, maak je eerst een eigen "branch": daarin kun je dan wijzigingen maken en naar GitHub sturen, zonder dat je met je klasgenoten in conflict raakt. Gebruik <kbd>Ctrl+Shift+P</kbd>, kies het commando "Git: Checkout to...", kies de optie "+ Create new branch..." en voer je eigen naam in als naam van de branch. Later kun je dit gebruiken om per nieuwe feature of set aan wijzigingen een branch aan te maken, maar voor nu kun je gewoon onder je eigen naam beginnen.

Een goed begin is met een aantal wijzigingen aan de *map*, die beschrijft hoe onze wereld eruit ziet. Open Tiled en open het bestand *resources/maps/main.tmx*. Sla het bestand op en voer de game opnieuw uit in Visual Studio Code om je gewijzigde game te spelen.
