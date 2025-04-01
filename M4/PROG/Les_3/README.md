# GD M4 PROG Les 3: Game Mechanics implementeren

#### Doel

Studenten leren hoe ze objecten in Unity laten bewegen met `Vector3` en botsingen detecteren met `collisions` en `triggers`, inclusief het verschil ertussen. Na de les kunnen ze een bewegend object maken dat reageert op botsingen.

#### Werkvorm

Klassiekale instructie en een demo in de les. Daarna verwerken met behulp van de volgende opdracht.

### Opdracht 3a: "Muntverzamelaar" (1,5 uur)

#### Doel

Maak een speler die beweegt met `Vector3` en munten verzamelt met een `trigger`.

#### Opdrachtbeschrijving

Maak een scène met een speler (cube) die beweegt met pijltjestoetsen en een munt (cube) die verdwijnt bij contact.

#### Stappen

1. **Setup (15 min)**

   - Nieuwe scène: speler-cube (met `Collider`), vloer-plane, munt-cube (met `Collider`, `Is Trigger` aan).
   - Maak script `PlayerMove.cs` en attach aan speler.

2. **Script schrijven (60 min)**

Er zijn 2 niveaus voor de opdracht om te differentieren: (beginner en gevorderd)

Open het script op je eigen niveau en voer de opdracht uit met de instructies in de comments:

[beginner script](SCRIPT_beginner.md)
[gevorderde script](SCRIPT_gevorderd.md)

![example 03](gfx/example_03.gif)

- Test: Beweeg naar de munt en zie hem verdwijnen.

3. **Uitbreiding (15 min)**

   - Voeg `Vector3.forward` toe met up/down pijltjes.
   - Maak `speed` public en test verschillende waarden.

4. **Inleveren**
   Lever de opdracht in door een readme te maken met daarin de volgende onderdelen verwerkt:
   - Titel van de opdracht
   - Omschrijving van de opdracht en wat je gedaan hebt
   - Gifje van de screencapture van je opdracht in unity
   - Afzonderlijke links naar de bijhorende scripts

Lever de link naar je readme in via de opdracht op simulise.

#### Beoordeling

- Beweegt de speler soepel?
- Wordt de munt opgepakt met een trigger?
