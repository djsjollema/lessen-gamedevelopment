# <span style="color: #000000;">Lesplan 1.2: Introductie Scripting in C#</span>

## <span style="color: #000000;">Lesoverzicht</span>

**Vak:** Game Development (Unity)  
**Vakcode:** GDV
**Les:** 1.2 - Introductie Scripting in C#  
**Duur:** 2 uur (45 min instructie + 75 min praktijk)  
**Doelgroep:** Beginners (MBO niveau 4)  
**Voorkennis:** Les 1.1 (Unity interface en projectstructuur)

## <span style="color: #000000;">Leerdoelen</span>

Na deze les kunnen studenten:

1. **Begrijpen** wat programmeren is en waarom het belangrijk is voor games
2. **Aanmaken** van een nieuw C# script in Unity
3. **Herkennen** en uitleggen van de basisstructuur van een C# script
4. **Gebruiken** van Debug.Log() om berichten te tonen in de Console
5. **Toepassen** van comments om code te documenteren
6. **Onderscheiden** tussen Start() en Update() functies

## <span style="color: #000000;">Lesopbouw</span>

### <span style="color: #000099;">DEEL 1: INSTRUCTIE (45 minuten)</span>

#### <span style="color: #000000;">Opening (3 minuten)</span>

**Activiteit:** Snelle terugblik en motivatie

- Korte recap van Les 1.1 (Unity interface)
- "Vandaag schrijven we onze eerste code!"
- "Code = instructies geven aan de computer"

#### <span style="color: #000000;">Hoofddeel 1: Wat is Programmeren? (7 minuten)</span>

**Activiteit:** Compacte uitleg met analogieën

**Inhoud:**

- Programmeren = instructies geven (pannenkoeken recept)
- Waarom in games? (beweging, vijanden, geluid)

**Interactie:**

- Snelle vraag: "Noem 3 dingen die geprogrammeerd zijn in jullie favoriete game?"

#### <span style="color: #000000;">Hoofddeel 2: Je Eerste Script (20 minuten)</span>

**Activiteit:** Hands-on demonstratie (studenten doen mee)

**Stappen:**

1. **Script aanmaken** (3 min)
   - Rechtsklik → Create → C# Script
   - Naam: `MijnEersteScript`
2. **Script openen & structuur** (12 min)

   - Dubbelklik om te openen
   - **Using statements:** "Gereedschapskisten"
   - **Class:** "Blauwdruk van vliegtuig"
   - **Start():** "Voorbereiding (1x)"
   - **Update():** "Flipbook (60x per seconde)"

3. **Debug.Log() implementeren** (5 min)
   ```csharp
   void Start()
   {
       Debug.Log("Hallo Unity! Dit is mijn eerste bericht!");
   }
   void Update()
   {
       Debug.Log("Hier is er nog een!");
   }
   ```

**Checkpoint:** Iedereen heeft werkende Debug.Log()

#### <span style="color: #000000;">Hoofddeel 3: Comments & Experimenteren (10 minuten)</span>

**Activiteit:** Korte uitleg + directe toepassing

**Inhoud:**

- Comments: `//` en `/* */`
- Waarom? (voor jezelf en teamleden)

**Voorbeeld:**

```csharp
void Start()
{
    // Welkomstbericht voor de speler
    Debug.Log("Game started");
    Debug.Log("Score: " + (10 + 5)); // Berekeningen werken ook!
}
```

#### <span style="color: #000000;">Afsluiting Instructie (5 minuten)</span>

**Activiteit:** Samenvatting en praktijkuitleg

1. **Snelle checklist:**

   - Script aanmaken ✓
   - Debug.Log() gebruiken ✓
   - Comments toevoegen ✓

2. **Praktijkuitleg:**
   - "Nu 75 minuten tijd voor oefeningen"
   - "Kies minimaal 1 oefening die past bij je niveau"
   - "Begin met Beginner-oefeningen als je twijfelt"
   - "Vraag hulp als je vastloopt!"

---

### <span style="color: #880000;">ENERGIZER: Code Corner Walk (5 minuten)</span>

**Activiteit:** Beweging door de klas om code-concepten te herhalen

**<span style="color: #000000;">Voorbereiding:</span>**
Wijs 4 hoeken/plekken in de klas aan:

- **Hoek 1:** "Start() Corner"
- **Hoek 2:** "Debug.Log() Corner"
- **Hoek 3:** "Comment Corner"
- **Hoek 4:** "Error Corner"

**Uitleg voor studenten:**
"We gaan onze benen strekken en tegelijk de code-concepten herhalen!"

**Spelregels:**

1. **Docent leest een situatie voor**
2. **Studenten lopen rustig naar de juiste hoek**
3. **Korte uitleg waarom die hoek klopt**

**Voorbeelden van situaties:**

- "Ik wil dat code één keer wordt uitgevoerd wanneer de game start" → Start() Corner
- "Ik wil een bericht tonen in de console" → Debug.Log() Corner
- "Ik wil uitleggen wat mijn code doet voor mezelf" → Comment Corner
- "Mijn code heeft een rode lijn en werkt niet" → Error Corner
- "Ik wil berekenen hoeveel 5 + 3 is en het tonen" → Debug.Log() Corner
- "Ik wil code schrijven die 60 keer per seconde herhaald wordt" → Update() Corner (pas hoek aan!)
- "Ik vergat een puntkomma aan het einde van mijn regel" → Error Corner
- "Ik wil tonen welke speler heeft gewonnen" → Debug.Log() Corner
- "Ik wil onthouden wat deze code doet als ik het over een maand weer bekijk" → Comment Corner
- "Ik wil de spelernaam één keer instellen aan het begin" → Start() Corner
- "Ik krijg een rood kronjeltje onder mijn tekst" → Error Corner
- "Ik wil live laten zien hoeveel punten de speler heeft" → Update() Corner
- "// Dit is tekst voor mezelf" → Comment Corner
- "Ik wil controleren of de speler nog leeft, elke frame" → Update() Corner
- "Visual Studio kan mijn code niet begrijpen" → Error Corner

**<span style="color: #000000;">Extra uitdagende voorbeelden (voor als studenten het snappen):</span>**

- "Time.deltaTime gebruiken voor smooth beweging" → Update() Corner
- "Een welkomstscherm tonen zodra de game opstart" → Start() Corner
- "/_ Multiline uitleg over complexe formule _/" → Comment Corner
- "NullReferenceException in de console" → Error Corner
- "Input.GetKey() controleren voor WASD beweging" → Update() Corner
- "Highscore laden uit een bestand bij opstarten" → Start() Corner

**<span style="color: #000000;">Tips voor de docent:</span>**

- Begin met makkelijke voorbeelden
- Als studenten twijfelen tussen hoeken → perfecte leermomenten!
- Laat studenten hun keuze uitleggen: "Waarom koos je deze hoek?"
- Mix praktische en theoretische voorbeelden
- Als het te makkelijk wordt → voeg Update() Corner toe of wissel hoeken om

**Doel:**

- Fysieke beweging zonder te veel aandacht
- Herhaling van geleerde concepten
- Klasgenoten ontmoeten tijdens het lopen
- Rustige voorbereiding op praktijkwerk

**Afsluiting energizer:**
"Perfect! Jullie snappen de concepten goed. Nu gaan we ze gebruiken in de praktijk. Ga terug naar je plek en kies een oefening die je leuk lijkt!"

---

### <span style="color: #008800;">DEEL 2: PRAKTIJK & OEFENINGEN (70 minuten)</span>

#### <span style="color: #000000;">Zelfstandig Werken (60 minuten)</span>

**Activiteit:** Studenten werken aan oefeningen

**<span style="color: #000000;">Docentrol:</span>**

- **Circuleren:** Loop tussen studenten
- **Hulp bieden:** Bij problemen direct helpen
- **Checkpoints:** Om de 15 min vragen "Hoe gaat het?"
- **Differentiatie:** Snelle leerlingen naar moeilijkere oefeningen

**<span style="color: #000000;">Studentactiviteiten:</span>**

- Kiezen van oefening (Beginner/Starter/Gevorderd)
- Script schrijven en testen
- README documentatie maken
- Experimenteren met eigen ideeën

#### <span style="color: #000000;">Afsluiting & Reflectie (10 minuten)</span>

**Activiteit:** Delen van resultaten

1. **<span style="color: #000000;">Showcase (5 min):</span>**

   - 2-3 studenten laten hun werk zien
   - "Wat heb je gemaakt en wat vond je leuk?"

2. **<span style="color: #000000;">Huiswerk & Vooruitblik (3 min):</span>**

   - "Werk af wat je nog niet af hebt"
   - "Upload naar GitHub"
   - "Volgende les: GameObjects bewegen!"

3. **<span style="color: #000000;">Evaluatie (2 min):</span>**

   - "Thumbs up/down: Vond je het leuk?"
   - "Waar liep je tegen aan?"

## <span style="color: #000000;">Materialen & Voorbereiding</span>

### <span style="color: #000000;">Voor de Docent:</span>

- [ ] Unity project klaar met lege scene
- [ ] Voorbeeld scripts voorbereid
- [ ] Console window zichtbaar
- [ ] Timer voor tijdmanagement
- [ ] Oefeningen lijst uitgeprint (backup)

### <span style="color: #000000;">Voor Studenten:</span>

- [ ] Unity geïnstalleerd
- [ ] Werkend Unity project van Les 1.1
- [ ] GitHub account (voor inlevering)
- [ ] Notitieblok/digitaal document

## <span style="color: #000000;">Differentiatie tijdens Praktijk</span>

### <span style="color: #000000;">Voor Snelle Leerlingen (na eerste oefening):</span>

- Probeer een Starter of Gevorderd oefening
- Experimenteer met Update() functie
- Help klasgenoten
- Voeg eigen creativiteit toe aan oefeningen

### <span style="color: #000000;">Voor Langzame Leerlingen:</span>

- Focus op 1 Beginner oefening
- Docent geeft extra 1-op-1 begeleiding
- Buddy-system met ervaren student

### <span style="color: #000000;">Voor Leerlingen met Leerproblemen:</span>

- Extra screenshots van verwachte resultaten
- Meer tijd voor basis Debug.Log() oefening
- Pauzeer regelmatig voor vragen

## <span style="color: #000000;">Evaluatie & Assessment</span>

### <span style="color: #000000;">Formatieve Evaluatie (tijdens praktijk):</span>

- **Rondlopen:** Observeren van werkende scripts
- **Directe feedback:** "Goed bezig!" of hulp bij fouten
- **Peer learning:** Studenten helpen elkaar

### <span style="color: #000000;">Summatieve Evaluatie (na les):</span>

- **Minimaal resultaat:** 1 werkende Debug.Log() script
- **Gewenst resultaat:** 1 complete oefening
- **Excellent resultaat:** Meerdere oefeningen + eigen creativiteit

### <span style="color: #000000;">Inlevering:</span>

- GitHub README met oefening documentatie
- Deadline: Voor volgende les

## <span style="color: #000000;">Veel Voorkomende Problemen & Snelle Oplossingen</span>

### <span style="color: #000000;">Script opent niet</span>

**Oplossing:**

- VS installer → Modify → Unity Gamedevelopment
- Unity → preferences → external tools → Visual Studio Community\*

### <span style="color: #000000;">Debug.Log() niet zichtbaar</span>

**Oplossing:** Window → General → Console + script op GameObject

### <span style="color: #000000;">Rode lijntjes/fouten</span>

**Oplossing:** Check `;` en spellingfouten, help student direct

### <span style="color: #000000;">"Ik snap er niks van"</span>

**Oplossing:** Terug naar basis, samen 1 regel schrijven

### <span style="color: #000000;">Studenten zijn te vroeg klaar</span>

**Oplossing:** Extra oefeningen, experimenteren, anderen helpen

## <span style="color: #000000;">Tijdmanagement Tips</span>

### <span style="color: #000000;">Als instructie te lang duurt:</span>

- Comments korter behandelen
- Minder experimenteren tijdens instructie
- Direct naar praktijk

### <span style="color: #000000;">Als studenten meer tijd nodig hebben:</span>

- Showcase verkorten
- Huiswerk verdelen over meerdere dagen
- Volgende les beginnen met Q&A

## <span style="color: #000000;">Huiswerk/Vervolgactiviteiten</span>

1. **Verplicht:**

   - Afmaken van gekozen oefening
   - Upload naar GitHub met README
   - Inleveren link op Simulise

2. **Optioneel:**

   - Extra oefeningen proberen
   - Experimenteren met eigen ideeën

3. **Voorbereiding volgende les:**
   - Nadenken: "Wat wil ik laten bewegen in een game?"

## <span style="color: #000000;">Reflectie voor Docent</span>

**<span style="color: #000000;">Direct na les evalueren:</span>**

- [ ] Lukte de timing van 45 min instructie?
- [ ] Hadden studenten genoeg tijd voor praktijk?
- [ ] Welke problemen kwamen het meest voor?
- [ ] Welke studenten hebben extra aandacht nodig?

**<span style="color: #000000;">Aanpassingen volgende keer:</span>**

- _Ruimte voor notities..._

---

**<span style="color: #000000;">Laatste update:</span>** 14-07-2025
**<span style="color: #000000;">Docent:</span>** Erwin Henraat
**<span style="color: #000000;">Versie:</span>** 1.0
