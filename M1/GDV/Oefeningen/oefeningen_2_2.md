# Oefeningen Les 2.2: Datatypes, Variabelen en Input

## Overzicht Oefeningen

Kies **minimaal 1 oefening** die past bij jouw niveau en interesse.

### Niveaus:

- ⭐ **Beginner** - Je eerste keer met variabelen

  - [Les2.2 Oefening 1B: Level Counter](#les22-oefening-1b-level-counter-)
  - [Les2.2 Oefening 2B: Score Tracker](#les22-oefening-2b-score-tracker-)
  - [Les2.2 Oefening 3B: Color Changer](#les22-oefening-3b-color-changer-)

- ⭐⭐ **Starter** - Je begrijpt variabelen en wilt input

  - [Les2.2 Oefening 4S: Simple Mover](#les22-oefening-4s-simple-mover-)
  - [Les2.2 Oefening 5S: Size Controller](#les22-oefening-5s-size-controller-)
  - [Les2.2 Oefening 6S: Spinner](#les22-oefening-6s-spinner-)

- ⭐⭐⭐ **Gevorderd** - Je wilt uitdaging met complexe variabelen
  - [Les2.2 Oefening 7G: Multi Control Object](#les22-oefening-7g-multi-control-object-)

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

## Les2.2 Oefening 1B: Level Counter ⭐

**Thema:** Level System

### Wat Ga Je Maken?

Een simpel level systeem waar je met toetsen je level kunt verhogen/verlagen en het GameObject omhoog/omlaag beweegt!

### Opdracht:

1. Maak een nieuw script: `LevelCounter`
2. Sleep het script op een Cube GameObject
3. Gebruik variabelen en input:

```csharp
public class LevelCounter : MonoBehaviour
{
    // Level variabelen
    public int level = 1;
    public string spelerNaam = "Player";

    // Positie variabelen
    private Vector3 startPositie;

    void Start()
    {
        startPositie = transform.position;

        Debug.Log("=== LEVEL COUNTER ===");
        Debug.Log("Speler: " + spelerNaam);
        Debug.Log("Start Level: " + level);
        Debug.Log("=== CONTROLS ===");
        Debug.Log("Druk op L = Level omhoog");
        Debug.Log("Druk op K = Level omlaag");
        Debug.Log("Druk op Space = Experience");
        Debug.Log("Druk op I = Info tonen");
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.L))
        {
            level = level + 1;
            Debug.Log("Level omhoog! Nieuw level: " + level);

            // Beweeg GameObject omhoog
            transform.position = startPositie + Vector3.up * level;
        }

        if (Input.GetKeyDown(KeyCode.K))
        {
            level = level - 1;
            if (level < 1) level = 1; // Niet lager dan level 1

            Debug.Log("Level omlaag! Nieuw level: " + level);

            // Beweeg GameObject omlaag
            transform.position = startPositie + Vector3.up * level;
        }

        if (Input.GetKeyDown(KeyCode.I))
        {
            Debug.Log("=== INFO ===");
            Debug.Log("Speler: " + spelerNaam);
            Debug.Log("Huidig level: " + level);
            Debug.Log("Positie: " + transform.position);
        }
    }
}
```

### Toevoegingen aan de code:

- Voeg een maximum level toe (bijvoorbeeld 10)
- Maak het GameObject ook groter per level
- Voeg experience points toe die je moet verzamelen door spatie te drukken
- Zorg dat je kubus harder draait naarmate je meer experience hebt
- Zorg dat je meer experience krijgt naar mate je in een hoger level komt
- Laat je experience zien als je op info drukt
- Zorg dat je experience betaalt om naar een hoger level te gaan
- als je onvoldoende experience hebt kun je niet naar een hoger level

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Les2.2 Oefening 2B: Simple Mover ⭐

**Thema:** Movement Control

### Wat Ga Je Maken?

Een bewegings controller waar je een GameObject kunt bewegen met WASD toetsen!

### Opdracht:

1. Maak een nieuw script: `SimpleMover`
2. Sleep het script op een GameObject naar keuze
3. Gebruik variabelen en input:

```csharp
public class SimpleMover : MonoBehaviour
{
    // Movement variabelen
    public string objectNaam = "Mover";

    // Positie tracking
    private Vector3 startPositie;
    private float totalAfstand = 0.0f;

    void Start()
    {
        startPositie = transform.position;
        Debug.Log("=== SIMPLE MOVER ===");
        Debug.Log("Object: " + objectNaam);

        Debug.Log("=== CONTROLS ===");
        Debug.Log("WASD = Bewegen");
        Debug.Log("Druk op I = Info");
        Debug.Log("Druk op H = Naar start positie");
    }

    void Update()
    {
        Vector3 oudePositie = transform.position;

        // WASD movement
        if (Input.GetKeyDown(KeyCode.W))
        {
            transform.position += transform.position + Vector3.forward;
        }
        if (Input.GetKey(KeyCode.S))
        {
            transform.position += transform.position + Vector3.back;
        }
        if (Input.GetKey(KeyCode.A))
        {
            transform.position += transform.position + Vector3.left;
        }
        if (Input.GetKey(KeyCode.D))
        {
            transform.position += transform.position + Vector3.right;
        }

        // Bereken afgelegde afstand
        float beweging = Vector3.Distance(oudePositie, transform.position);
        totalAfstand = totalAfstand + beweging;

        if (Input.GetKeyDown(KeyCode.I))
        {
            Debug.Log("=== INFO ===");
            Debug.Log("Huidige positie: " + transform.position);
            Debug.Log("Totale afstand: " + totalAfstand);
        }

        if (Input.GetKeyDown(KeyCode.H))
        {
            transform.position = startPositie;
            totalAfstand = 0.0f;
            Debug.Log("Terug naar start!");
        }
    }
}
```

### Toevoegingen aan de code:

- Voeg Q/E toe voor omhoog/omlaag bewegen
- Maak een variabele voor de snelheid die je in kunt stellen in de inspector
- Maak het object 2x sneller met wanneer je Shift inhoud
- Tel het aantal keer dat je een stap hebt gezet en voeg dit toe aan je info
- Zorg dat het spel afgelopen is als je 20 stappen hebt gezet

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Les2.2 Oefening 3B: Size Controller ⭐

**Thema:** Scale Control

### Wat Ga Je Maken?

Een grootte controller waar je een GameObject groter en kleiner kunt maken met toetsen!

### Opdracht:

1. Maak een nieuw script: `SizeController`
2. Sleep het script op een GameObject naar keuze
3. Gebruik variabelen en input:

```csharp
public class SizeController : MonoBehaviour
{
    // Size variabelen
    public float grootte = 1.0f;
    public float verandering = 0.1f;
    public string objectNaam = "Scaler";

    // Schaal tracking
    private Vector3 startSchaal;

    void Start()
    {
        startSchaal = transform.localScale;

        Debug.Log("=== SIZE CONTROLLER ===");
        Debug.Log("Object: " + objectNaam);
        Debug.Log("Start grootte: " + grootte);
        Debug.Log("=== CONTROLS ===");
        Debug.Log("Druk op + = Groter");
        Debug.Log("Druk op - = Kleiner");
        Debug.Log("Druk op R = Reset grootte");
        Debug.Log("Druk op I = Info");
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Plus) || Input.GetKeyDown(KeyCode.Equals))
        {
            grootte = grootte + verandering;
            Debug.Log("Groter! Nieuwe grootte: " + grootte);

            // Pas schaal aan
            transform.localScale = startSchaal * grootte;
        }

        if (Input.GetKeyDown(KeyCode.Minus))
        {
            grootte = grootte - verandering;
            if (grootte < 0.1f) grootte = 0.1f; // Niet te klein

            Debug.Log("Kleiner! Nieuwe grootte: " + grootte);

            // Pas schaal aan
            transform.localScale = startSchaal * grootte;
        }

        if (Input.GetKeyDown(KeyCode.R))
        {
            grootte = 1.0f;
            transform.localScale = startSchaal;
            Debug.Log("Grootte gereset!");
        }

        if (Input.GetKeyDown(KeyCode.I))
        {
            Debug.Log("=== INFO ===");
            Debug.Log("Huidige grootte: " + grootte);
            Debug.Log("Huidige schaal: " + transform.localScale);
        }


    }
}
```

### Toevoegingen aan de code:

- Voeg maximum en minimum grootte toe
- Roteer het object met de pijltjes (links en rechts)
- Verplaats het object om hoog en omlaag met de pijltjes (omhoog en omlaag)

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Les2.2 Oefening 4S: Spinner ⭐⭐

**Thema:** Rotation Control

### Wat Ga Je Maken?

Een draai controller waar je een GameObject kunt laten draaien met toetsen!

### Opdracht:

1. Maak een nieuw script: `Spinner`
2. Sleep het script op een GameObject naar keuze
3. Gebruik variabelen en input:

```csharp
public class Spinner : MonoBehaviour
{
    // Rotatie variabelen
    public float draaiSnelheid = 45.0f; // graden per seconde
    public bool isDraaiend = false;
    public string spinnerNaam = "Spinner";

    // Rotatie tracking
    private float totalRotatie = 0.0f;

    void Start()
    {
        Debug.Log("=== SPINNER ===");
        Debug.Log("Spinner: " + spinnerNaam);
        Debug.Log("Draai snelheid: " + draaiSnelheid + " graden/sec");
        Debug.Log("=== CONTROLS ===");
        Debug.Log("Spatie = Start/Stop draaien");
        Debug.Log("Druk op L = Draai links");
        Debug.Log("Druk op R = Draai rechts");
        Debug.Log("Druk op I = Info");
    }

    void Update()
    {
        // Automatisch draaien als isDraaiend true is
        if (isDraaiend)
        {
            float rotatie = draaiSnelheid * Time.deltaTime;
            transform.Rotate(0, rotatie, 0);
            totalRotatie = totalRotatie + rotatie;
        }

        if (Input.GetKeyDown(KeyCode.Space))
        {
            isDraaiend = !isDraaiend; // Wissel tussen true en false

            if (isDraaiend)
            {
                Debug.Log("Start met draaien!");
            }
            else
            {
                Debug.Log("Stop met draaien!");
            }
        }

        if (Input.GetKeyDown(KeyCode.L))
        {
            transform.Rotate(0, -45, 0); // 45 graden naar links
            totalRotatie = totalRotatie + 45;
            Debug.Log("Draai naar links!");
        }

        if (Input.GetKeyDown(KeyCode.R))
        {
            transform.Rotate(0, 45, 0); // 45 graden naar rechts
            totalRotatie = totalRotatie + 45;
            Debug.Log("Draai naar rechts!");
        }

        if (Input.GetKeyDown(KeyCode.I))
        {
            Debug.Log("=== INFO ===");
            Debug.Log("Is draaiend: " + isDraaiend);
            Debug.Log("Totale rotatie: " + totalRotatie + " graden");
            Debug.Log("Huidige rotatie: " + transform.rotation.eulerAngles);
        }
    }
}
```

### Toevoegingen aan de code:

- Voeg sneller/langzamer draaien toe met toetsen (UP en Down)
- Zorg voor een minimum en maximum draaisnelheid
- Wissel de as waarover het object draait als je op de spatie drukt
- Zorg dat je bij de info ook ziet op welke as je draait
- Tel hoeveel volledige rondes (360 graden) het object heeft gemaakt
- Laat bij info zien hoeveel rondjes je hebt gedraaid

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Les2.2 Oefening 7G: Multi Control Object ⭐⭐⭐

**Thema:** Combined Controls

### Wat Ga Je Maken?

Een object dat je volledig kunt besturen: bewegen, grootte veranderen, draaien en kleur veranderen!

### Opdracht:

1. Maak een nieuw script: `MultiController`
2. Sleep het script op een GameObject naar keuze
3. Gebruik alle technieken samen:

```csharp
public class MultiController : MonoBehaviour
{
    // Object info
    public string objectNaam = "Multi Controller";

    // Movement
    public float bewegingsSnelheid = 3.0f;
    private Vector3 startPositie;

    // Scale
    public float grootte = 1.0f;
    private Vector3 startSchaal;

    // Rotation
    public float draaiSnelheid = 90.0f;
    public bool isDraaiend = false;

    // Color
    public string huidigeKleur = "Wit";

    // Stats
    private float totalAfstand = 0.0f;
    private float totalRotatie = 0.0f;

    void Start()
    {
        startPositie = transform.position;
        startSchaal = transform.localScale;

        Debug.Log("=== MULTI CONTROLLER ===");
        Debug.Log("Object: " + objectNaam);
        Debug.Log("=== CONTROLS ===");
        Debug.Log("WASD = Bewegen");
        Debug.Log("+/- = Grootte");
        Debug.Log("Spatie = Draaien aan/uit");
        Debug.Log("1-5 = Kleuren");
        Debug.Log("R = Reset alles");
        Debug.Log("I = Info");
    }

    void Update()
    {
        // MOVEMENT
        Vector3 oudePositie = transform.position;

        if (Input.GetKey(KeyCode.W))
        {
            transform.position = transform.position + Vector3.forward * bewegingsSnelheid * Time.deltaTime;
        }
        if (Input.GetKey(KeyCode.S))
        {
            transform.position = transform.position + Vector3.back * bewegingsSnelheid * Time.deltaTime;
        }
        if (Input.GetKey(KeyCode.A))
        {
            transform.position = transform.position + Vector3.left * bewegingsSnelheid * Time.deltaTime;
        }
        if (Input.GetKey(KeyCode.D))
        {
            transform.position = transform.position + Vector3.right * bewegingsSnelheid * Time.deltaTime;
        }

        // Track afstand
        totalAfstand = totalAfstand + Vector3.Distance(oudePositie, transform.position);

        // SIZE
        if (Input.GetKeyDown(KeyCode.Plus) || Input.GetKeyDown(KeyCode.Equals))
        {
            grootte = grootte + 0.2f;
            transform.localScale = startSchaal * grootte;
            Debug.Log("Groter! Grootte: " + grootte);
        }
        if (Input.GetKeyDown(KeyCode.Minus))
        {
            grootte = grootte - 0.2f;
            if (grootte < 0.2f) grootte = 0.2f;
            transform.localScale = startSchaal * grootte;
            Debug.Log("Kleiner! Grootte: " + grootte);
        }

        // ROTATION
        if (isDraaiend)
        {
            float rotatie = draaiSnelheid * Time.deltaTime;
            transform.Rotate(0, rotatie, 0);
            totalRotatie = totalRotatie + rotatie;
        }

        if (Input.GetKeyDown(KeyCode.Space))
        {
            isDraaiend = !isDraaiend;
            Debug.Log("Draaien: " + isDraaiend);
        }

        // COLORS
        if (Input.GetKeyDown(KeyCode.Alpha1))
        {
            GetComponent<Renderer>().material.color = Color.red;
            huidigeKleur = "Rood";
            Debug.Log("Kleur: " + huidigeKleur);
        }
        if (Input.GetKeyDown(KeyCode.Alpha2))
        {
            GetComponent<Renderer>().material.color = Color.green;
            huidigeKleur = "Groen";
            Debug.Log("Kleur: " + huidigeKleur);
        }
        if (Input.GetKeyDown(KeyCode.Alpha3))
        {
            GetComponent<Renderer>().material.color = Color.blue;
            huidigeKleur = "Blauw";
            Debug.Log("Kleur: " + huidigeKleur);
        }
        if (Input.GetKeyDown(KeyCode.Alpha4))
        {
            GetComponent<Renderer>().material.color = Color.yellow;
            huidigeKleur = "Geel";
            Debug.Log("Kleur: " + huidigeKleur);
        }
        if (Input.GetKeyDown(KeyCode.Alpha5))
        {
            GetComponent<Renderer>().material.color = Color.white;
            huidigeKleur = "Wit";
            Debug.Log("Kleur: " + huidigeKleur);
        }

        // RESET
        if (Input.GetKeyDown(KeyCode.R))
        {
            transform.position = startPositie;
            transform.localScale = startSchaal;
            transform.rotation = Quaternion.identity;
            grootte = 1.0f;
            isDraaiend = false;
            totalAfstand = 0.0f;
            totalRotatie = 0.0f;
            GetComponent<Renderer>().material.color = Color.white;
            huidigeKleur = "Wit";
            Debug.Log("Alles gereset!");
        }

        // INFO
        if (Input.GetKeyDown(KeyCode.I))
        {
            Debug.Log("=== OBJECT INFO ===");
            Debug.Log("Positie: " + transform.position);
            Debug.Log("Grootte: " + grootte);
            Debug.Log("Kleur: " + huidigeKleur);
            Debug.Log("Draaiend: " + isDraaiend);
            Debug.Log("Totale afstand: " + totalAfstand);
            Debug.Log("Totale rotatie: " + totalRotatie + " graden");
        }
    }
}
```

### Toevoegingen aan de code:

- Voeg geluid effecten toe (Debug.Log verschillende geluiden)
- Maak presets (T-toets zet alles op een vooraf ingestelde configuratie)
- Voeg een "random" modus toe die alles willekeurig verandert

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)
transform.position += Vector3.right _ snelheid _ Time.deltaTime;
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

````

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
````

### Toevoegingen aan de code:

- Voeg achievements systeem toe (bijv. "100 jumps")
- Maak een high score systeem
- Voeg power-ups toe die tijdelijk stats veranderen
- Bereken efficiency scores (score per seconde, etc.)

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)
