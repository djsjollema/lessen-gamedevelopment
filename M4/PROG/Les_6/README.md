# GD M4 PROG Les 6: Vector3 verdieping

#### Doel

Studenten leren hoe `Vector3` werkt in Unity voor posities, richtingen en beweging, met focus op `Lerp` (soepele overgangen), `Distance` (afstand meten), `magnitude` (vectorlengte), en `Normalize`/`normalized` (eenheidsvectoren). Na de les kunnen ze een object verplaatsen, meten, en richting normaliseren.

#### Werkvorm

Klassiekale instructie en een demo in de les. Daarna verwerken met behulp van de volgende opdracht.

### Opdracht 6: "Volger" (1,5 uur)

#### Doel

Met deze opdracht zorg je dat je iets een ander object kan laten volgen en met een soepele beweging ook weer terug naar het startpunt beweegt.

#### Opdrachtbeschrijving

Maak een scène waarin een "volger" (sphere) de "speler" (cube) volgt met `Vector3.Lerp`. Als de speler bereikt is beweegt de volger weer terug naar zijn start positie met een constante snelheid.

Laat de speler met pijltjestoetsen bewegen over de x- en z-as.

De afstand tussen de volger en de speler en de afstand tussen de volger en het startpunt wordt opgemeten. Zo kan er geschakeld worden tussen volgen en teruggaan.

#### Stappen

1. **Setup (15 min)**

   - Nieuwe scène: speler-cube op `(0, 0, 0)`, volger-sphere op afstand bijvoorbeeld `(5, 2, 0)`, vloer-plane.
   - Maak script `PlayerMove.cs`attach aan speler (cube)
   - Maak script `FollowAndReturn.cs` attach aan volger (sphere).

2. **Script schrijven (60 min)**

Er zijn 2 niveaus voor de opdracht om te differentieren: (beginner en gevorderd)

Open het script op je eigen niveau en voer de opdracht uit met de instructies in de comments:

[beginner script](SCRIPT_beginner.md)
[gevorderde script](SCRIPT_gevorderd.md)

![example 06](gfx/example_06.gif)

- Test: Loop rond met de Speler. Beweegt de follower achter je aan? beweegt de follower weer terug als hij de speler heeft bereikt?

3. **Uitbreiding (15 min)**
   - Plaats een blok in je scene (dummy)
   - Zorg dat de speler kogels af kan vuren die vanzelf achter de dummy aangaan. (homing missles)
   - Beweeg de dummy heen en weer over het veld.
   - Gebruik dezelfde technieken die je in de opdracht al hebt gebruikt.

![example 06_2](gfx/example_06_2.gif)

4. **Inleveren**
   Lever de opdracht in door een readme te maken met daarin de volgende onderdelen verwerkt:
   - Titel van de opdracht
   - Omschrijving van de opdracht en wat je gedaan hebt
   - Gifje van de screencapture van je opdracht in unity
   - Afzonderlijke links naar de bijhorende scripts

Lever de link naar je readme in via de opdracht op simulise.

#### Beoordeling

- Beweegt de speler met pijltjes
- Volgt de volger de speler via `Lerp`?
- beweegt de volger weer terug met een vaste snelheid?
- Worden `Distance` of `magnitude`, en `normalized` correct gebruikt?
- Is er ook nog een homing missle en een dummy die heen en weer gaat?
