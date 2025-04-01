# GD M4 PROG Les 1: Basisprogrammeren in C#

#### Doel

Studenten leren de basis van programmeren in C# binnen Unity: variabelen, if-statements, loops, functies en collections. Na de les kunnen ze deze vaardigheden toepassen in een eenvoudige Unity-opdracht.

#### Werkvorm

Klassiekale instructie en een demo in de les. Daarna verwerken met behulp van de volgende opdracht.

### Opdracht 1: "Score en Munten" (1,5 uur)

#### Doel

Studenten maken een simpel Unity-script dat een score bijhoudt, munten verzamelt en een win-conditie checkt, met gebruik van alle vaardigheden uit deze les.

#### Opdrachtbeschrijving

Maak een Unity-scène met een speler (een simpele cube) en een script genaamd `PlayerScore`. Het script moet:

1. Een **score** bijhouden met een variabele.
2. Een **if-statement** gebruiken om te checken of de speler wint (score ≥ 50).
3. Een **loop** gebruiken om bij de start 3 berichten te tonen.
4. Een **functie** maken om munten toe te voegen aan een lijst.
5. Een **collection (List)** gebruiken om munten te verzamelen.

#### Stappen

1. **Setup (10 min)**

   - Maak een nieuwe Unity-scène.
   - Voeg een cube toe als "speler" en attach een nieuw script `PlayerScore.cs`.

2. **Script schrijven (60 min)**
   Er zijn 2 niveaus voor de opdracht om te differentieren: (beginner en gevorderd)

   Open het script op je eigen niveau en voer de opdracht uit met de instructies in de comments:

   [beginner script](SCRIPT_beginner.md)
   [gevorderde script](SCRIPT_gevorderd.md)

- Test in Unity: druk op spatie om munten toe te voegen en kijk of je wint bij 50.

3. **Uitbreiding (20 min)**

   - Maak `score` en `coins` public en bekijk ze in de Inspector.
   - Voeg een bericht toe dat het aantal munten toont (bijv. `Debug.Log("Aantal munten: " + coins.Count);`).

4. **Inleveren**
   Lever de opdracht in door een readme te maken met daarin de volgende onderdelen verwerkt:
   - Titel van de opdracht
   - Omschrijving van de opdracht en wat je gedaan hebt
   - Gifje van de screencapture van je opdracht in unity
   - Afzonderlijke links naar de bijhorende scripts

Lever de link naar je readme in via de opdracht op simulise.

#### Beoordeling

- Werkt de score en win-conditie?
- Worden munten correct toegevoegd aan de lijst?
- Wordt de loop bij de start uitgevoerd?
- Is de functie bruikbaar en logisch?
