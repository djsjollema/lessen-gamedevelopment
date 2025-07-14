# Oefeningen Les 2.2: Datatypes, Variabelen en Input

## Overzicht Oefeningen

Kies **minimaal 1 oefening** die past bij jouw niveau en interesse.

### Niveaus:

- ⭐ **Beginner** - Je eerste keer met variabelen

  - [Les2.2 Oefening 1B: Gaming Profile Creator](#les22-oefening-1b-gaming-profile-creator-)
  - [Les2.2 Oefening 2B: Simple Calculator](#les22-oefening-2b-simple-calculator-)
  - [Les2.2 Oefening 3B: Virtual Pet Stats](#les22-oefening-3b-virtual-pet-stats-)

- ⭐⭐ **Starter** - Je begrijpt variabelen en wilt input

  - [Les2.2 Oefening 4S: Keyboard Piano](#les22-oefening-4s-keyboard-piano-)
  - [Les2.2 Oefening 5S: Character Name Generator](#les22-oefening-5s-character-name-generator-)
  - [Les2.2 Oefening 6S: Simple Movement Controller](#les22-oefening-6s-simple-movement-controller-)

- ⭐⭐⭐ **Gevorderd** - Je wilt uitdaging met complexe variabelen
  - [Les2.2 Oefening 7G: Interactive Game Stats Dashboard](#les22-oefening-7g-interactive-game-stats-dashboard-)

---

## Algemene Inlever Instructies

### Voor Elke Oefening:

1. **Script file** - Upload je .cs bestand naar GitHub
2. **README documentatie** - Verwerk je opdracht in je README met titel, beschrijving, gif en code link
3. **GitHub repository** - Zorg dat je project beschikbaar is op GitHub en dat je de link naar je readme hebt ingeleverd op simulise.

### Success Tips:

- Begin met een oefening die past bij jouw niveau en interesse
- Experimenteer gerust met verschillende datatypes
- Test je variabelen door ze te wijzigen in de Inspector
- Vraag hulp als je vastloopt - dat is normaal!

---

## Les2.2 Oefening 1B: Gaming Profile Creator ⭐

**Thema:** Gaming Profielen

### Wat Ga Je Maken?

Een script dat jouw gaming profiel toont met verschillende variabelen én reageert op input om je profiel aan te passen! Het GameObject beweegt ook omhoog als je level stijgt!

### Opdracht:

1. Maak een nieuw script: `GamingProfile`
2. Sleep het script op een Cube GameObject
3. Gebruik verschillende datatypes voor je profiel en voeg input toe:

```csharp
public class GamingProfile : MonoBehaviour
{
    // Gaming profiel variabelen (public zodat je ze in Inspector kunt aanpassen)
    public string gamerTag = "ProGamer2024";
    public int level = 42;
    public float speelTijd = 127.5f;
    public bool isOnline = true;
    public int aantalWins = 89;
    public int aantalLosses = 23;

    // Visuele feedback variabelen
    private Vector3 startPositie;
    private float levelHoogte = 0.5f; // Hoeveel omhoog per level

    void Start()
    {
        startPositie = transform.position;
        
        // Zet GameObject op juiste hoogte gebaseerd op level
        transform.position = startPositie + Vector3.up * (level * levelHoogte);

        Debug.Log("=== GAMING PROFIEL ===");
        Debug.Log("Gamertag: " + gamerTag);
        Debug.Log("Level: " + level);
        Debug.Log("Speeltijd: " + speelTijd + " uur");
        Debug.Log("Online status: " + isOnline);
        Debug.Log("Wins: " + aantalWins);
        Debug.Log("Losses: " + aantalLosses);

        // Bereken win percentage
        float winPercentage = (aantalWins * 100.0f) / (aantalWins + aantalLosses);
        Debug.Log("Win percentage: " + winPercentage.ToString("F1") + "%");

        Debug.Log("=== CONTROLS ===");
        Debug.Log("Druk op P = Profiel tonen");
        Debug.Log("Druk op L = Level omhoog (GameObject beweegt omhoog!)");
        Debug.Log("Druk op W = Win toevoegen (GameObject wordt groter!)");
        Debug.Log("Druk op O = Online status wisselen (GameObject kleur verandert!)");
    }

    void Update()
    {
        // Input verwerking
        if (Input.GetKeyDown(KeyCode.P))
        {
            Debug.Log("=== GAMING PROFIEL ===");
            Debug.Log("Gamertag: " + gamerTag);
            Debug.Log("Level: " + level);
            Debug.Log("Speeltijd: " + speelTijd + " uur");
            Debug.Log("Online status: " + isOnline);
            Debug.Log("Wins: " + aantalWins);
            Debug.Log("Losses: " + aantalLosses);

            // Bereken win percentage
            float winPercentage = (aantalWins * 100.0f) / (aantalWins + aantalLosses);
            Debug.Log("Win percentage: " + winPercentage.ToString("F1") + "%");
        }

        if (Input.GetKeyDown(KeyCode.L))
        {
            level++;
            Debug.Log("Level omhoog! Nieuw level: " + level);
            
            // Beweeg GameObject omhoog per level
            transform.position = startPositie + Vector3.up * (level * levelHoogte);
        }

        if (Input.GetKeyDown(KeyCode.W))
        {
            aantalWins++;
            Debug.Log("Win toegevoegd! Totaal wins: " + aantalWins);
            
            // Maak GameObject groter bij elke win
            float schaalFactor = 1.0f + (aantalWins * 0.01f);
            transform.localScale = Vector3.one * schaalFactor;
        }

        if (Input.GetKeyDown(KeyCode.O))
        {
            isOnline = !isOnline; // Wissel tussen true en false
            Debug.Log("Online status gewijzigd naar: " + isOnline);
            
            // Verander de kleur van het GameObject (als het een Renderer heeft)
            Renderer objectRenderer = GetComponent<Renderer>();
            if (objectRenderer != null)
            {
                if (isOnline)
                {
                    objectRenderer.material.color = Color.green; // Online = groen
                }
                else
                {
                    objectRenderer.material.color = Color.red; // Offline = rood
                }
            }
        }
    }
}
```

### Toevoegingen aan de code:

- Voeg rotatie toe: draai het GameObject als je een loss toevoegt
- Maak het GameObject "bouncy" door het omhoog en omlaag te laten bewegen
- Voeg een reset functie toe die alles terugzet naar de startpositie

---

## Les2.2 Oefening 2B: Simple Calculator ⭐

**Thema:** Wiskunde en Berekeningen

### Wat Ga Je Maken?

Een interactieve calculator die reageert op toetsenbordinvoer om verschillende berekeningen uit te voeren! De resultaten worden ook visueel getoond door het GameObject te bewegen!

### Opdracht:

1. Maak een nieuw script: `SimpleCalculator`
2. Sleep het script op een Sphere GameObject
3. Gebruik variabelen voor berekeningen en input voor interactie:

```csharp
public class SimpleCalculator : MonoBehaviour
{
    // Calculator variabelen
    public float getal1 = 15.0f;
    public float getal2 = 7.0f;
    
    // Visuele feedback
    private Vector3 startPositie;

    void Start()
    {
        startPositie = transform.position;
        
        Debug.Log("=== SIMPLE CALCULATOR ===");
        Debug.Log("Getal 1: " + getal1);
        Debug.Log("Getal 2: " + getal2);
        Debug.Log("=== CONTROLS ===");
        Debug.Log("+ = Optellen (GameObject beweegt omhoog)");
        Debug.Log("- = Aftrekken (GameObject beweegt omlaag)");
        Debug.Log("* = Vermenigvuldigen (GameObject wordt groter)");
        Debug.Log("/ = Delen (GameObject wordt kleiner)");
        Debug.Log("R = Nieuwe random getallen (GameObject naar start)");
        Debug.Log("C = Alle berekeningen tonen");
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Plus))
        {
            float resultaat = getal1 + getal2;
            Debug.Log(getal1 + " + " + getal2 + " = " + resultaat);
            
            // Beweeg GameObject omhoog gebaseerd op resultaat
            transform.position = transform.position + Vector3.up * (resultaat * 0.01f);
        }
        
        if (Input.GetKeyDown(KeyCode.Minus))
        {
            float resultaat = getal1 - getal2;
            Debug.Log(getal1 + " - " + getal2 + " = " + resultaat);
            
            // Beweeg GameObject omlaag
            transform.position = transform.position + Vector3.down * (resultaat * 0.01f);
        }
        
        if (Input.GetKeyDown(KeyCode.Asterisk))
        {
            float resultaat = getal1 * getal2;
            Debug.Log(getal1 + " × " + getal2 + " = " + resultaat);
            
            // Maak GameObject groter gebaseerd op resultaat
            float schaalFactor = 1.0f + (resultaat * 0.001f);
            transform.localScale = Vector3.one * schaalFactor;
        }

        if (Input.GetKeyDown(KeyCode.Slash))
        {
            if (getal2 != 0) // Controleer of we niet delen door 0
            {
                float resultaat = getal1 / getal2;
                Debug.Log(getal1 + " ÷ " + getal2 + " = " + resultaat.ToString("F2"));
                
                // Maak GameObject kleiner
                float schaalFactor = Mathf.Max(0.1f, 1.0f - (resultaat * 0.01f));
                transform.localScale = Vector3.one * schaalFactor;
            }
            else
            {
                Debug.Log("Error: Kan niet delen door 0!");
                
                // Laat GameObject trillen bij error
                transform.position = startPositie + new Vector3(
                    Random.Range(-0.1f, 0.1f),
                    Random.Range(-0.1f, 0.1f),
                    Random.Range(-0.1f, 0.1f)
                );
            }
        }

        if (Input.GetKeyDown(KeyCode.R))
        {
            // Genereer nieuwe random getallen
            getal1 = Random.Range(1.0f, 100.0f);
            getal2 = Random.Range(1.0f, 100.0f);
            Debug.Log("Nieuwe getallen: " + getal1.ToString("F1") + " en " + getal2.ToString("F1"));
            
            // Reset GameObject naar start positie en schaal
            transform.position = startPositie;
            transform.localScale = Vector3.one;
        }

        if (Input.GetKeyDown(KeyCode.C))
        {
            // Optelling
            float resultaatOptellen = getal1 + getal2;
            Debug.Log(getal1 + " + " + getal2 + " = " + resultaatOptellen);
            
            // Beweeg GameObject omhoog voor optelling
            transform.position = transform.position + Vector3.up * (resultaatOptellen * 0.01f);
            
            // Aftrekking
            float resultaatAftrekken = getal1 - getal2;
            Debug.Log(getal1 + " - " + getal2 + " = " + resultaatAftrekken);
            
            // Beweeg GameObject omlaag voor aftrekking
            transform.position = transform.position + Vector3.down * (resultaatAftrekken * 0.01f);
            
            // Vermenigvuldiging
            float resultaatVermenigvuldigen = getal1 * getal2;
            Debug.Log(getal1 + " × " + getal2 + " = " + resultaatVermenigvuldigen);
            
            // Maak GameObject groter voor vermenigvuldiging
            float schaalFactor = 1.0f + (resultaatVermenigvuldigen * 0.001f);
            transform.localScale = Vector3.one * schaalFactor;

            // Delen
            if (getal2 != 0) // Controleer op deling door 0
            {
                float resultaatDelen = getal1 / getal2;
                Debug.Log(getal1 + " ÷ " + getal2 + " = " + resultaatDelen.ToString("F2"));
                
                // Maak GameObject kleiner voor deling
                float schaalFactorDelen = Mathf.Max(0.1f, 1.0f - (resultaatDelen * 0.01f));
                transform.localScale = Vector3.one * schaalFactorDelen;
            }
            else
            {
                Debug.Log("Error: Kan niet delen door 0!");
            }
            
            // Draai GameObject rond tijdens het tonen van alle berekeningen
            transform.Rotate(0, 90, 0);
        }
    }
}
```

### Toevoegingen aan de code:

- Voeg min berekening toe met de (Minus)-toets
- Voeg vermenigvuldiging toe met de (Asterisk)-toets
- Voeg modulo berekening toe (restwaarde na deling) met de (Percent)-toets
- Zorg dat je alle berekeningen in 1x doet als je op de C-toets drukt

---

## Les2.2 Oefening 3B: Virtual Pet Stats ⭐

**Thema:** Virtual Pets en Tamagochi

### Wat Ga Je Maken?

Een interactief virtueel huisdier dat reageert op jouw input en waarvan je de stats kunt aanpassen! Het GameObject reageert visueel op de mood van je huisdier!

### Opdracht:

1. Maak een nieuw script: `VirtualPet`
2. Sleep het script op een Capsule GameObject (dit wordt je huisdier)
3. Gebruik variabelen voor pet statistieken en input voor interactie:

```csharp
public class VirtualPet : MonoBehaviour
{
    // Huisdier basis info
    public string petNaam = "Fluffy";
    public string petSoort = "Kat";
    public int petLeeftijd = 3;
    public float petGewicht = 4.2f;

    // Huisdier stats (0-100)
    public int honger = 75;
    public int energie = 60;
    public int geluk = 85;
    public bool slaapt = false;
    
    // Visuele feedback
    private Vector3 startPositie;
    private Vector3 startSchaal;

    void Start()
    {
        startPositie = transform.position;
        startSchaal = transform.localScale;
        
        UpdateVisueleStatus();

        Debug.Log("=== " + petNaam.ToUpper() + " STATUS ===");
        Debug.Log("Soort: " + petSoort + " | Leeftijd: " + petLeeftijd + " jaar");
        Debug.Log("Gewicht: " + petGewicht + " kg");
        Debug.Log("Honger: " + honger + "/100");
        Debug.Log("Energie: " + energie + "/100");
        Debug.Log("Geluk: " + geluk + "/100");
        Debug.Log("Slaapt: " + slaapt);

        // Bereken algemene gezondheid
        float gezondheid = (float)(100 - honger + energie + geluk) / 3.0f;
        Debug.Log("Algehele gezondheid: " + gezondheid.ToString("F1") + "/100");

        Debug.Log("=== CONTROLS ===");
        Debug.Log("F = Voeren (honger -20, GameObject springt omhoog!)");
        Debug.Log("S = Slapen (energie +30, GameObject wordt plat!)");
        Debug.Log("P = Spelen (geluk +15, GameObject danst!)");
        Debug.Log("I = Status tonen");
    }

    void Update()
    {
        // Input verwerking
        if (Input.GetKeyDown(KeyCode.F))
        {
            honger = honger - 20;
            if (honger < 0) honger = 0; // Niet lager dan 0

            Debug.Log(petNaam + " heeft gegeten! Honger nu: " + honger);
            
            // Laat huisdier "springen" van blijdschap
            transform.position = startPositie + Vector3.up * 2.0f;
            
            UpdateVisueleStatus();
        }

        if (Input.GetKeyDown(KeyCode.S))
        {
            if (!slaapt)
            {
                slaapt = true;
                energie = energie + 30;
                if (energie > 100) energie = 100; // Niet hoger dan 100

                Debug.Log(petNaam + " gaat slapen... Energie nu: " + energie);
                
                // Maak huisdier plat (slaapt)
                transform.localScale = new Vector3(startSchaal.x * 1.5f, startSchaal.y * 0.3f, startSchaal.z * 1.5f);
                transform.position = new Vector3(startPositie.x, startPositie.y - 0.5f, startPositie.z);
            }
            else
            {
                slaapt = false;
                Debug.Log(petNaam + " wordt wakker!");
                
                // Herstel normale vorm
                transform.localScale = startSchaal;
                transform.position = startPositie;
            }
        }

        if (Input.GetKeyDown(KeyCode.P))
        {
            if (energie > 10)
            {
                geluk = geluk + 15;
                energie = energie - 10;

                if (geluk > 100) geluk = 100;

                Debug.Log("Je speelt met " + petNaam + "! Geluk: " + geluk + ", Energie: " + energie);
                
                // Laat huisdier "dansen" (draaien)
                transform.Rotate(0, 180, 0);
                
                UpdateVisueleStatus();
            }
            else
            {
                Debug.Log(petNaam + " is te moe om te spelen!");
                
                // Laat huisdier langzaam zakken (moe)
                transform.position = startPositie + Vector3.down * 0.5f;
            }
        }

        if (Input.GetKeyDown(KeyCode.I))
        {
            Debug.Log("=== " + petNaam.ToUpper() + " STATUS ===");
            Debug.Log("Soort: " + petSoort + " | Leeftijd: " + petLeeftijd + " jaar");
            Debug.Log("Gewicht: " + petGewicht + " kg");
            Debug.Log("Honger: " + honger + "/100");
            Debug.Log("Energie: " + energie + "/100");
            Debug.Log("Geluk: " + geluk + "/100");
            Debug.Log("Slaapt: " + slaapt);

            // Bereken algemene gezondheid
            float gezondheid = (float)(100 - honger + energie + geluk) / 3.0f;
            Debug.Log("Algehele gezondheid: " + gezondheid.ToString("F1") + "/100");

            UpdateVisueleStatus();
        }
        
        // Laat huisdier langzaam terugkeren naar normale positie
        if (!slaapt)
        {
            transform.position = Vector3.Lerp(transform.position, startPositie, Time.deltaTime * 2.0f);
        }
    }
    
    void UpdateVisueleStatus()
    {
        // Verander kleur gebaseerd op geluk
        Renderer petRenderer = GetComponent<Renderer>();
        if (petRenderer != null)
        {
            if (geluk > 80)
            {
                petRenderer.material.color = Color.green; // Gelukkig = groen
            }
            else if (geluk > 40)
            {
                petRenderer.material.color = Color.yellow; // Oké = geel
            }
            else
            {
                petRenderer.material.color = Color.red; // Verdrietig = rood
            }
        }
        
        // Verander grootte gebaseerd op honger
        float hongerSchaal = 0.8f + (honger / 100.0f) * 0.4f; // Tussen 0.8 en 1.2
        if (!slaapt)
        {
            transform.localScale = startSchaal * hongerSchaal;
        }
    }
}
```

### Toevoegingen aan de code:

- Voeg een "ziek" status toe die het GameObject laat trillen
- Maak een "gelukkig" animatie waarbij het GameObject op en neer beweegt
- Voeg geluiden toe (Debug.Log verschillende geluiden zoals "Miauw!" of "Woof!")

---

## Les2.2 Oefening 4S: Keyboard Piano ⭐⭐

**Thema:** Muziek en Input

### Wat Ga Je Maken?

Een virtuele piano die reageert op toetsenbordinvoer - elke toets speelt een "noot"!

### Opdracht:

1. Maak een nieuw script: `KeyboardPiano`
2. Gebruik Input.GetKeyDown() voor piano toetsen:

```csharp
public class KeyboardPiano : MonoBehaviour
{
    // Piano instellingen
    public string pianistNaam = "Mozart Jr.";
    public bool isOpgenomen = false;

    void Start()
    {
        Debug.Log("=== KEYBOARD PIANO ===");
        Debug.Log("Pianist: " + pianistNaam);
        Debug.Log("Druk op QWERTYUI voor piano noten!");
        Debug.Log("Spatie = Sustain pedaal");
    }

    void Update()
    {
        // Piano toetsen (C-D-E-F-G-A-B-C)
        if (Input.GetKeyDown(KeyCode.Q))
        {
            Debug.Log("♪ C noot gespeeld!");
        }
        if (Input.GetKeyDown(KeyCode.W))
        {
            Debug.Log("♪ D noot gespeeld!");
        }
        if (Input.GetKeyDown(KeyCode.E))
        {
            Debug.Log("♪ E noot gespeeld!");
        }
        if (Input.GetKeyDown(KeyCode.R))
        {
            Debug.Log("♪ F noot gespeeld!");
        }
        if (Input.GetKeyDown(KeyCode.T))
        {
            Debug.Log("♪ G noot gespeeld!");
        }
        if (Input.GetKeyDown(KeyCode.Y))
        {
            Debug.Log("♪ A noot gespeeld!");
        }
        if (Input.GetKeyDown(KeyCode.U))
        {
            Debug.Log("♪ B noot gespeeld!");
        }
        if (Input.GetKeyDown(KeyCode.I))
        {
            Debug.Log("♪ C (hoog) noot gespeeld!");
        }

        // Sustain pedaal
        if (Input.GetKey(KeyCode.Space))
        {
            Debug.Log("🎵 Sustain pedaal ingedrukt");
        }
    }
}
```

### Toevoegingen aan de code:

- Voeg een teller toe voor hoeveel noten je hebt gespeeld
- Maak verschillende "instrumenten" (piano, gitaar, drums)
- Tel hoelang elke noot wordt "vastgehouden"

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Les2.2 Oefening 5S: Character Name Generator ⭐⭐

**Thema:** RPG en Character Creation

### Wat Ga Je Maken?

Een character generator die nieuwe namen maakt elke keer dat je een toets indrukt!

### Opdracht:

1. Maak een nieuw script: `CharacterGenerator`
2. Gebruik variabelen en input voor character generation:

```csharp
public class CharacterGenerator : MonoBehaviour
{
    // Character eigenschappen
    public string huidigeNaam = "Onbekend";
    public string huidigeKlasse = "Avonturier";
    public int huidigLevel = 1;
    public int aantalGenerated = 0;

    void Start()
    {
        Debug.Log("=== CHARACTER NAME GENERATOR ===");
        Debug.Log("Druk op G = Genereer nieuw character");
        Debug.Log("Druk op S = Toon statistieken");
        Debug.Log("Druk op R = Reset generator");

        GenereerCharacter();
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.G))
        {
            GenereerCharacter();
        }

        if (Input.GetKeyDown(KeyCode.S))
        {
            ToonStatistieken();
        }

        if (Input.GetKeyDown(KeyCode.R))
        {
            ResetGenerator();
        }
    }

    void GenereerCharacter()
    {
        // Simpele naam generator met variabelen
        int randomNummer = Random.Range(1, 5);

        if (randomNummer == 1)
        {
            huidigeNaam = "Thorin";
            huidigeKlasse = "Strijder";
        }
        else if (randomNummer == 2)
        {
            huidigeNaam = "Elara";
            huidigeKlasse = "Magiër";
        }
        else if (randomNummer == 3)
        {
            huidigeNaam = "Kael";
            huidigeKlasse = "Boogschutter";
        }
        else
        {
            huidigeNaam = "Zara";
            huidigeKlasse = "Dief";
        }

        huidigLevel = Random.Range(1, 21);
        aantalGenerated++;

        Debug.Log("=== NIEUW CHARACTER ===");
        Debug.Log("Naam: " + huidigeNaam);
        Debug.Log("Klasse: " + huidigeKlasse);
        Debug.Log("Level: " + huidigLevel);
        Debug.Log("Character #" + aantalGenerated);
    }

    void ToonStatistieken()
    {
        Debug.Log("=== GENERATOR STATS ===");
        Debug.Log("Totaal characters: " + aantalGenerated);
        Debug.Log("Huidige character: " + huidigeNaam);
    }

    void ResetGenerator()
    {
        aantalGenerated = 0;
        Debug.Log("Generator gereset!");
    }
}
```

### Toevoegingen aan de code:

- Voeg meer namen en klasses toe
- Maak character stats (kracht, intelligentie, etc.)
- Tel gemiddeld level van alle characters

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Les2.2 Oefening 6S: Simple Movement Controller ⭐⭐

**Thema:** Character Movement

### Wat Ga Je Maken?

Een movement controller die een GameObject laat bewegen met WASD toetsen en statistieken bijhoudt!

### Opdracht:

1. Maak een nieuw script: `SimpleMovement`
2. Gebruik Input en variabelen voor beweging:

```csharp
public class SimpleMovement : MonoBehaviour
{
    // Movement variabelen
    public float snelheid = 5.0f;
    public string spelerNaam = "Hero";

    // Statistiek variabelen
    private float totalAfstand = 0.0f;
    private int aantalBewegingen = 0;
    private Vector3 startPositie;

    void Start()
    {
        startPositie = transform.position;

        Debug.Log("=== MOVEMENT CONTROLLER ===");
        Debug.Log("Speler: " + spelerNaam);
        Debug.Log("Snelheid: " + snelheid);
        Debug.Log("Gebruik WASD om te bewegen");
        Debug.Log("Druk op I voor info");
    }

    void Update()
    {
        Vector3 oudePositie = transform.position;
        bool heeftBewogen = false;

        // WASD movement
        if (Input.GetKey(KeyCode.W))
        {
            transform.position += Vector3.forward * snelheid * Time.deltaTime;
            heeftBewogen = true;
        }
        if (Input.GetKey(KeyCode.S))
        {
            transform.position += Vector3.back * snelheid * Time.deltaTime;
            heeftBewogen = true;
        }
        if (Input.GetKey(KeyCode.A))
        {
            transform.position += Vector3.left * snelheid * Time.deltaTime;
            heeftBewogen = true;
        }
        if (Input.GetKey(KeyCode.D))
        {
            transform.position += Vector3.right * snelheid * Time.deltaTime;
            heeftBewogen = true;
        }

        // Statistieken bijwerken
        if (heeftBewogen)
        {
            float bewegingsAfstand = Vector3.Distance(oudePositie, transform.position);
            totalAfstand += bewegingsAfstand;
            aantalBewegingen++;
        }

        // Info tonen
        if (Input.GetKeyDown(KeyCode.I))
        {
            Vector3 huidigePositie = transform.position;
            float afstandVanStart = Vector3.Distance(startPositie, huidigePositie);

            Debug.Log("=== MOVEMENT INFO ===");
            Debug.Log("Speler: " + spelerNaam);
            Debug.Log("Huidige positie: " + huidigePositie);
            Debug.Log("Totale afstand gelopen: " + totalAfstand.ToString("F1"));
            Debug.Log("Afstand van start: " + afstandVanStart.ToString("F1"));
            Debug.Log("Aantal bewegings-frames: " + aantalBewegingen);
        }
    }
}
```

### Toevoegingen aan de code:

- Voeg sprint functie toe (Shift = sneller)
- Tel tijd dat speler stil staat vs beweegt
- Voeg Y-as beweging toe (Q/E voor omhoog/omlaag)

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Les2.2 Oefening 7G: Interactive Game Stats Dashboard ⭐⭐⭐

**Thema:** Advanced Game Statistics

### Wat Ga Je Maken?

Een interactief dashboard dat real-time game statistieken bijhoudt en reageert op verschillende inputs!

### Opdracht:

1. Maak een nieuw script: `GameStatsDashboard`
2. Gebruik complexe variabelen en input voor een volledig dashboard:

```csharp
public class GameStatsDashboard : MonoBehaviour
{
    [Header("Speler Info")]
    public string spelerNaam = "Pro Player";
    public int spelerLevel = 1;
    public float ervaring = 0.0f;
    public float ervaringNodig = 100.0f;

    [Header("Game Stats")]
    public int score = 0;
    public int levens = 3;
    public float speelTijd = 0.0f;
    public bool gameActief = true;

    [Header("Performance Tracking")]
    private int aantalActions = 0;
    private int aantalJumps = 0;
    private int aantalAttacks = 0;
    private float laatsteActionTijd = 0.0f;
    private float snelsteAction = float.MaxValue;

    void Start()
    {
        Debug.Log("=== GAME STATS DASHBOARD ===");
        Debug.Log("Speler: " + spelerNaam + " (Level " + spelerLevel + ")");
        Debug.Log("=== CONTROLS ===");
        Debug.Log("SPACE = Jump | X = Attack | + = Score | - = Damage");
        Debug.Log("L = Level Up | R = Reset Stats | I = Info");
        ToonDashboard();
    }

    void Update()
    {
        if (gameActief)
        {
            speelTijd += Time.deltaTime;

            // Input handling met performance tracking
            if (Input.GetKeyDown(KeyCode.Space))
            {
                PerformAction("Jump");
                aantalJumps++;
                Debug.Log("💫 Jump! (Totaal: " + aantalJumps + ")");
            }

            if (Input.GetKeyDown(KeyCode.X))
            {
                PerformAction("Attack");
                aantalAttacks++;
                score += 10;
                Debug.Log("⚔️ Attack! Score: " + score);
            }

            if (Input.GetKeyDown(KeyCode.Plus) || Input.GetKeyDown(KeyCode.Equals))
            {
                score += 50;
                ervaring += 25.0f;
                CheckLevelUp();
                Debug.Log("🎯 Bonus Score! Total: " + score);
            }

            if (Input.GetKeyDown(KeyCode.Minus))
            {
                levens--;
                Debug.Log("💔 Damage taken! Levens: " + levens);
                if (levens <= 0)
                {
                    GameOver();
                }
            }

            if (Input.GetKeyDown(KeyCode.L))
            {
                LevelUp();
            }

            if (Input.GetKeyDown(KeyCode.I))
            {
                ToonDashboard();
            }

            if (Input.GetKeyDown(KeyCode.R))
            {
                ResetStats();
            }
        }

        // Game restart
        if (!gameActief && Input.GetKeyDown(KeyCode.Return))
        {
            RestartGame();
        }
    }

    void PerformAction(string actionType)
    {
        aantalActions++;
        float huidigeTijd = Time.time;

        if (laatsteActionTijd > 0)
        {
            float tijdTussenActions = huidigeTijd - laatsteActionTijd;
            if (tijdTussenActions < snelsteAction)
            {
                snelsteAction = tijdTussenActions;
            }
        }

        laatsteActionTijd = huidigeTijd;
    }

    void CheckLevelUp()
    {
        if (ervaring >= ervaringNodig)
        {
            LevelUp();
        }
    }

    void LevelUp()
    {
        spelerLevel++;
        ervaring = 0.0f;
        ervaringNodig += 50.0f; // Meer ervaring nodig per level
        levens++; // Bonus leven bij level up

        Debug.Log("🌟 LEVEL UP! Nieuw level: " + spelerLevel);
        Debug.Log("✨ Bonus leven gekregen! Levens: " + levens);
    }

    void ToonDashboard()
    {
        float ervaringPercentage = (ervaring / ervaringNodig) * 100.0f;
        float actionsPerMinuut = (aantalActions / (speelTijd / 60.0f));

        Debug.Log("=== DASHBOARD UPDATE ===");
        Debug.Log("👤 " + spelerNaam + " | Level: " + spelerLevel);
        Debug.Log("🎯 Score: " + score + " | ❤️ Levens: " + levens);
        Debug.Log("⭐ Ervaring: " + ervaring.ToString("F0") + "/" + ervaringNodig + " (" + ervaringPercentage.ToString("F1") + "%)");
        Debug.Log("⏱️ Speeltijd: " + speelTijd.ToString("F1") + " seconden");
        Debug.Log("🏃 Jumps: " + aantalJumps + " | ⚔️ Attacks: " + aantalAttacks);
        Debug.Log("📊 Actions/minuut: " + actionsPerMinuut.ToString("F1"));
        if (snelsteAction < float.MaxValue)
        {
            Debug.Log("⚡ Snelste action: " + snelsteAction.ToString("F2") + " sec");
        }
    }

    void GameOver()
    {
        gameActief = false;
        float finalAPM = (aantalActions / (speelTijd / 60.0f));

        Debug.Log("=== GAME OVER ===");
        Debug.Log("💀 " + spelerNaam + " is verslagen!");
        Debug.Log("📊 Final Score: " + score);
        Debug.Log("⏱️ Overlevingstijd: " + speelTijd.ToString("F1") + " seconden");
        Debug.Log("🎯 Level bereikt: " + spelerLevel);
        Debug.Log("📈 Actions per minuut: " + finalAPM.ToString("F1"));
        Debug.Log("🔄 Druk ENTER om opnieuw te beginnen");
    }

    void ResetStats()
    {
        score = 0;
        ervaring = 0.0f;
        aantalActions = 0;
        aantalJumps = 0;
        aantalAttacks = 0;
        speelTijd = 0.0f;
        snelsteAction = float.MaxValue;
        laatsteActionTijd = 0.0f;

        Debug.Log("🔄 Stats gereset!");
        ToonDashboard();
    }

    void RestartGame()
    {
        gameActief = true;
        levens = 3;
        spelerLevel = 1;
        ervaringNodig = 100.0f;
        ResetStats();

        Debug.Log("🎮 Game herstart! Veel succes " + spelerNaam + "!");
    }
}
```

### Toevoegingen aan de code:

- Voeg achievements systeem toe (bijv. "100 jumps")
- Maak een high score systeem
- Voeg power-ups toe die tijdelijk stats veranderen
- Bereken efficiency scores (score per seconde, etc.)

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)
