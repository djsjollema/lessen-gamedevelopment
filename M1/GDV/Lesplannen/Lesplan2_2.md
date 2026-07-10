# <span style="color: #000000;">Lesplan 2.2: Datatypes, Variabelen en Input</span>

## <span style="color: #000000;">Lesoverzicht</span>

**Vak:** Game Development (Unity)  
**Vakcode:** GDV  
**Les:** 2.2 - Datatypes, Variabelen en Input  
**Duur:** 2 uur (50 min instructie + 70 min praktijk)  
**Doelgroep:** Beginners (MBO niveau 4)  
**Voorkennis:** Les 2.1 (Unity basics, Transform, eerste scripts)

## <span style="color: #000000;">Leerdoelen</span>

Na deze les kunnen studenten:

1. **Begrijpen** wat variabelen zijn en waarom ze essentieel zijn voor games
2. **Toepassen** van de 4 belangrijkste datatypes (int, float, string, bool)
3. **Gebruiken** van assignment en rekenkundige operatoren
4. **Implementeren** van if statements en vergelijkingsoperatoren
5. **Verwerken** van toetsenbordinput met GetKey(), GetKeyDown() en GetAxis()
6. **Maken** van een eenvoudig bewegingssysteem
7. **Gebruiken** van public variabelen in de Unity Inspector

## <span style="color: #000000;">Lesopbouw</span>

### <span style="color: #000099;">DEEL 1: INSTRUCTIE (50 minuten)</span>

#### <span style="color: #000000;">Opening (5 minuten)</span>

**Activiteit:** Motiverende start met concrete voorbeelden

- "Wat houdt een game bij over jou als speler?" (score, leven, items)
- "Vandaag leren we hoe we die informatie opslaan en gebruiken!"
- Korte recap: "Vorige les maakten we scripts - nu gaan we ze slim maken"

#### <span style="color: #000000;">Hoofddeel 1: Variabelen Concept (8 minuten)</span>

**Activiteit:** Interactieve uitleg met analogieën

**Inhoud:**

- Variabelen = gelabelde dozen voor informatie
- Waarom nodig in games? (speler stats, game state, beweging)

**Interactie:**

- "Roep een getal!" → "Die waarde stop ik in variabele 'getal'"
- "Wat wil je bijhouden in je favoriete game?"

**Demo:** Live voorbeeld met simpele variabele in Unity

```csharp
int score = 0;
Debug.Log("Score: " + score);
```

#### <span style="color: #000000;">Hoofddeel 2: Datatypes (12 minuten)</span>

**Activiteit:** Hands-on met elk datatype

**Structuur per datatype (3 min elk):**

1. **Int** - hele getallen
2. **Float** - kommagetallen (met f!)
3. **String** - tekst (met aanhalingstekens)
4. **Bool** - waar/onwaar

**Live Coding:** Studenten typen mee

```csharp
void Start()
{
    int leven = 100;
    float snelheid = 5.5f;
    string naam = "Player";
    bool gameOver = false;

    Debug.Log("Naam: " + naam + ", Leven: " + leven);
}
```

**Checkpoint:** Iedereen heeft werkende variabelen

#### <span style="color: #000000;">Hoofddeel 3: Operatoren (10 minuten)</span>

**Activiteit:** Praktische voorbeelden met game-context

**Assignment operator (3 min):**

- `=` betekent "ken toe", niet "is gelijk aan"

**Rekenkundige operatoren (4 min):**

- Live demo: `+ - * / %`
- Game voorbeeld: score berekenen

**Kortere schrijfwijzen (3 min):**

- `+=`, `++` etc.
- "Snelkoppelingen voor luie programmeurs!"

```csharp
int score = 100;
score += 50;    // Kills
score *= 2;     // Multiplier
score++;        // Bonus point
```

#### <span style="color: #000000;">Hoofddeel 4: Input & If Statements (15 minuten)</span>

**Activiteit:** Van theorie naar interactieve game

**If statements (5 min):**

- Analogie: "Als het regent, neem paraplu mee"
- Vergelijkingsoperatoren: `> < >= <= ==`

**Input.GetKey() (5 min):**

- Live demo: WASD movement detection
- Verschil GetKey() vs GetKeyDown()

**Input.GetAxis() (5 min):**

- Vloeiende beweging
- Gamepad-ready

```csharp
void Update()
{
    if (Input.GetKey(KeyCode.W))
        Debug.Log("Moving forward!");

    float horizontal = Input.GetAxis("Horizontal");
    Debug.Log("Move: " + horizontal);
}
```

**Checkpoint:** Studenten hebben werkende input detection

---

### <span style="color: #880000;">ENERGIZER: Variable Type Simon Says (8 minuten)</span>

**Activiteit:** Bewegingsspel om datatypes te versterken

**Voorbereiding:**

- Maak 4 zones in de klas: "Int Corner", "Float Corner", "String Corner", "Bool Corner"

**Spelregels:**

1. **Docent roept een waarde** (bijvoorbeeld: "42", "3.14f", "Hello", "true")
2. **Studenten lopen naar de juiste corner**
3. **Snelste team krijgt punt**

**Voorbeelden:**

- "100" → Int Corner
- "5.5f" → Float Corner
- "Game Over" → String Corner
- "false" → Bool Corner
- "score += 10" → Int Corner (resultaat)
- "temperature == 98.6f" → Bool Corner (vergelijking)

**Variaties:**

- Code snippets laten zien
- Foutieve syntax (niemand beweegt)
- "Simon Says" regel toevoegen

**Doel:** Versterken van datatype herkenning door beweging

---

### <span style="color: #008800;">DEEL 2: PRAKTIJK & OEFENINGEN (62 minuten)</span>

#### <span style="color: #000000;">Bewegingssysteem Demo (10 minuten)</span>

**Activiteit:** Gezamenlijk een movement script bouwen

**Stappen:**

1. **Nieuw script:** `SimpleMovement`
2. **Variables:** `float snelheid = 5.0f;`
3. **Input handling:** WASD detection
4. **Position update:** `transform.position`

**Resultaat:** Werkend bewegingssysteem dat studenten kunnen uitbreiden

#### <span style="color: #000000;">Zelfstandig Werken (45 minuten)</span>

**Activiteit:** Studenten werken aan oefeningen naar keuze

**Docentrol:**

- **Circuleren:** Help bij problemen
- **Differentiatie:** Verschillende moeilijkheidsniveaus
- **Checkpoints:** Om de 15 min voortgang checken

**Studentactiviteiten:**

- Kies oefening (Beginner/Intermediate/Advanced)
- Experimenteren met variabelen en input
- Documenteren in README

#### <span style="color: #000000;">Showcase & Reflectie (7 minuten)</span>

**Activiteit:** Delen van resultaten

1. **Demo's (4 min):** 2-3 studenten tonen hun werk
2. **Reflection (2 min):** "Wat was moeilijk? Wat was leuk?"
3. **Wrap-up (1 min):** Huiswerk en volgende les preview

## <span style="color: #000000;">Materialen & Voorbereiding</span>

### <span style="color: #000000;">Voor de Docent:</span>

- [ ] Unity project met lege scene
- [ ] Voorbeeld scripts voorbereid
- [ ] Console window zichtbaar
- [ ] Input settings gecontroleerd (Input Manager = Old)
- [ ] Timer voor tijdmanagement
- [ ] Energizer zones gemarkeerd

### <span style="color: #000000;">Voor Studenten:</span>

- [ ] Unity geïnstalleerd en werkend
- [ ] Code editor (Visual Studio) gekoppeld
- [ ] GitHub account voor inlevering
- [ ] Notitieblok/digitaal document

## <span style="color: #000000;">Differentiatie</span>

### <span style="color: #000000;">Voor Snelle Leerlingen:</span>

- Probeer meerdere oefeningen
- Experimenteer met GetAxis() in plaats van GetKey()
- Voeg eigen creativiteit toe (kleuren, geluiden via Debug.Log)
- Help klassgenoten

### <span style="color: #000000;">Voor Langzame Leerlingen:</span>

- Focus op 1 basis oefening
- Extra begeleiding bij datatypes
- Buddy-system met ervaren student
- Gebruik visuele hulpmiddelen (datatype cheat sheet)

### <span style="color: #000000;">Voor Leerlingen met Problemen:</span>

- Screenshots van verwachte resultaten
- Stap-voor-stap checklist
- Meer tijd voor fundamentals
- 1-op-1 begeleiding tijdens praktijk

## <span style="color: #000000;">Assessment & Evaluatie</span>

### <span style="color: #000000;">Formatieve Evaluatie:</span>

- **Checkpoints:** Werkende code na elk hoofddeel
- **Energizer:** Begrip van datatypes
- **Rondlopen:** Observatie tijdens praktijk
- **Peer feedback:** Studenten helpen elkaar

### <span style="color: #000000;">Summatieve Evaluatie:</span>

- **Minimaal:** 1 werkend script met variabelen en input
- **Gewenst:** 1 complete oefening met documentatie
- **Excellent:** Meerdere oefeningen + eigen toevoegingen

### <span style="color: #000000;">Inlevering:</span>

- GitHub README met oefening documentatie
- Link naar werkende Unity project
- Deadline: Voor volgende les

## <span style="color: #000000;">Troubleshooting & Oplossingen</span>

### <span style="color: #000000;">Input werkt niet</span>

**Symptoom:** GetKey() geeft errors  
**Oplossing:** Edit → Project Settings → Active Input Handling → "Input Manager (Old)"

### <span style="color: #000000;">Float syntax problemen</span>

**Symptoom:** Errors bij `float snelheid = 5.5`  
**Oplossing:** Voeg `f` toe: `float snelheid = 5.5f`

### <span style="color: #000000;">Movement te snel/langzaam</span>

**Symptoom:** GameObject beweegt vreemd  
**Oplossing:** Gebruik `Time.deltaTime` en pas snelheid aan

### <span style="color: #000000;">Public variabelen niet zichtbaar</span>

**Symptoom:** Inspector toont geen variabelen  
**Oplossing:** Check `public` keyword en script is attached

### <span style="color: #000000;">"Ik snap er niets van"</span>

**Oplossing:** Terug naar basics, samen 1 variabele maken

## <span style="color: #000000;">Tijdmanagement</span>

### <span style="color: #000000;">Als instructie te lang duurt:</span>

- Operatoren korter behandelen
- Input demo inkorten
- Meer focus op hands-on

### <span style="color: #000000;">Als studenten meer tijd nodig hebben:</span>

- Showcase verkorten naar 5 min
- Huiswerk spreiden over meer dagen
- Energizer overslaan indien nodig

### <span style="color: #000000;">Als studenten vroeg klaar zijn:</span>

- Extra uitdagingen uit oefeningen
- Help anderen
- Experimenteer met nieuwe concepten

## <span style="color: #000000;">Huiswerk & Vervolgactiviteiten</span>

### <span style="color: #000000;">Verplicht:</span>

1. Afmaken van gekozen oefening
2. GitHub README met documentatie
3. Upload werkend Unity project
4. Inleveren via Simulise

### <span style="color: #000000;">Optioneel:</span>

1. Extra oefeningen proberen
2. Experimenteren met andere KeyCodes
3. Eigen movement ideeën uitwerken

### <span style="color: #000000;">Voorbereiding volgende les:</span>

- Nadenken: "Welke GameObjects wil je laten bewegen?"
- Bekijk: Basis physics concepten (zwaartekracht, botsingen)

## <span style="color: #000000;">Belangrijke Aandachtspunten</span>

### <span style="color: #000000;">Technische Setup:</span>

- **Input Manager:** Controleer vóór les dat oude input system actief is
- **Visual Studio:** Zorg dat code completion werkt
- **Project Settings:** Backup project voor snelle recovery

### <span style="color: #000000;">Pedagogische Focus:</span>

- **Concrete voorbeelden:** Gebruik altijd game-gerelateerde voorbeelden
- **Hands-on:** Laat studenten meerdere keren mee-typen
- **Fouten normaliseren:** "Fouten maken hoort bij programmeren!"
- **Succeservaringen:** Zorg dat iedereen iets werkends heeft

### <span style="color: #000000;">Klassenbeheer:</span>

- **Tempo afstemmen:** Check of langzame leerlingen meekomen
- **Energie monitoren:** Gebruik energizer als concentratie afneemt
- **Hulp organiseren:** Stimuleer peer-to-peer learning

## <span style="color: #000000;">Reflectie voor Docent</span>

**<span style="color: #000000;">Direct na les evalueren:</span>**

- [ ] Begrepen studenten de datatypes?
- [ ] Lukte de input handling voor iedereen?
- [ ] Was de energizer effectief?
- [ ] Welke problemen kwamen het meest voor?
- [ ] Hadden studenten genoeg praktijktijd?

**<span style="color: #000000;">Verbeterpunten volgende keer:</span>**

- _Ruimte voor notities..._

---

**<span style="color: #000000;">Laatste update:</span>** [Datum]  
**<span style="color: #000000;">Docent:</span>** [Naam]  
**<span style="color: #000000;">Versie:</span>** 1.0
