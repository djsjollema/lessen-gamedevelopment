# Oefeningen Les 1.2: Introductie Scripting in C#

## Overzicht Oefeningen

Kies **minimaal 1 oefening** die past bij jouw niveau en interesse. Elke oefening heeft een ander thema uit de populaire cultuur!

### Niveaus:

- ⭐ **Beginner** - Je eerste keer programmeren
- ⭐⭐ **Starter** - Je begrijpt de basis al een beetje
- ⭐⭐⭐ **Gevorderd** - Je wilt meer uitdaging
- ⭐⭐⭐⭐ **Expert** - Je bent al handig met code
- ⭐⭐⭐⭐⭐ **Master** - Breng me naar mijn limiet!

---

## Oefening 1: Spotify Playlist Generator ⭐

**Thema:** Muziek en Streaming

### Wat Ga Je Maken?

Een script dat je favoriete muziekliedjes "afspeelt"(niet echt) door ze in de console te loggen, net zoals een Spotify playlist!

### Opdracht:

1. Maak een nieuw script: `SpotifyPlaylist`
2. In de `Start()` functie, log je favoriete liedjes:

```csharp
void Start()
{
    // Welkomstbericht
    Debug.Log("Welkom bij jouw Spotify Playlist!");
    Debug.Log("Nu aan het afspelen:");

    // Log 5 van je favoriete liedjes
    Debug.Log(" 1. [Artiest] - [Liedje naam]");
    Debug.Log(" 2. [Artiest] - [Liedje naam]");
    // Voeg er zelf nog 3 toe!

    Debug.Log(" Playlist voltooid! Geniet van je muziek!");
}
```

### Toevoegingen aan de code:

- Voeg het jaar van het liedje toe
- Tel hoeveel liedjes je hebt (gebruik cijfers in je berichten)
- Maak 2 verschillende playlists voor verschillende stemmingen

### Inlever Vereisten:

- Screenshot van je console output
- Korte uitleg: "Ik heb geleerd hoe ik Debug.Log() gebruik om berichten te tonen"

---

## Oefening 2: Gaming Setup Configurator ⭐⭐

**Thema:** Gaming Hardware

### Wat Ga Je Maken?

Een script dat jouw ultieme gaming setup beschrijft, inclusief berekeningen van totaalprijs!

### Opdracht:

1. Maak een nieuw script: `GamingSetup`
2. Gebruik comments om je code te organiseren:

```csharp
void Start()
{
    // === WELKOMSTBERICHT ===
    Debug.Log(" Welkom bij de Gaming Setup Configurator! ");

    // === HARDWARE SPECS ===
    Debug.Log(" Monitor: [Jouw favoriete gaming monitor]");
    Debug.Log(" Controller: [Xbox/PlayStation/andere]");
    Debug.Log(" Headset: [Jouw headset merk]");

    // === PRIJSBEREKENING ===
    // Gebruik variabelen voor prijzen (dit leer je later, dus vul gewoon getallen in)
    Debug.Log(" Monitor prijs: €" + 299);
    Debug.Log(" Controller prijs: €" + 69);
    Debug.Log(" Headset prijs: €" + 149);

    // Bereken totaal
    Debug.Log(" TOTAAL: €" + (299 + 69 + 149));

    // === EINDRESULTAAT ===
    Debug.Log(" Je gaming setup is compleet! Game on!");
}
```

### Toevoegingen aan de code:

- Voeg meer hardware toe (toetsenbord, muis, webcam)
- Bereken korting percentages
- Maak verschillende budget opties (budget/premium/ultra)

### Inlever Vereisten:

- Screenshot van console met jouw complete setup
- Uitleg over hoe je comments hebt gebruikt om je code te organiseren

---

## 📱 Oefening 3: Social Media Dashboard ⭐⭐⭐

**Thema:** Social Media en Influencers

### 🎯 Wat Ga Je Maken?

Een dashboard dat verschillende social media statistieken toont, met realtime updates in de Update functie!

### 📝 Opdracht:

1. Maak een nieuw script: `SocialMediaDashboard`
2. Gebruik zowel `Start()` als `Update()`:

```csharp
void Start()
{
    // === ACCOUNT SETUP ===
    Debug.Log("📱 Social Media Dashboard Gestart!");
    Debug.Log("👤 Account: @[jouw_username]");
    Debug.Log("📊 Dashboard geladen...");

    // === STATISTIEKEN ===
    Debug.Log("📈 Instagram followers: " + 1247);
    Debug.Log("🐦 Twitter followers: " + 892);
    Debug.Log("📺 YouTube subscribers: " + 15600);
    Debug.Log("💃 TikTok followers: " + 3421);

    // === RECENT ACTIVITEIT ===
    Debug.Log("🔥 Laatste post: 23 likes in 5 minuten!");
    Debug.Log("💬 Nieuwe comments: 7");
}

void Update()
{
    // Deze code toont live updates (elke seconde ongeveer)
    // LET OP: Dit maakt veel berichten! Test maar kort.

    // Toon alleen elke 60 frames (ongeveer 1x per seconde)
    if (Time.frameCount % 60 == 0)
    {
        Debug.Log("🔔 Live update - Frame: " + Time.frameCount + " | Online gebruikers: " + Random.Range(100, 500));
    }
}
```

### ✅ Bonus Uitdagingen:

- Voeg meer social media platforms toe
- Simuleer follower groei over tijd
- Maak verschillende soorten posts (foto/video/story)
- Bereken engagement rates

### 🏆 Inlever Vereisten:

- Screenshot die zowel Start() als Update() berichten toont
- Korte uitleg over het verschil tussen Start() en Update()

---

## 🚗 Oefening 4: Dream Car Configurator ⭐⭐⭐⭐

**Thema:** Auto's en Lifestyle

### 🎯 Wat Ga Je Maken?

Een uitgebreide auto configurator die verschillende opties toont en complexe berekeningen doet!

### 📝 Opdracht:

1. Maak een nieuw script: `DreamCarConfigurator`
2. Gebruik geavanceerde string combinaties en berekeningen:

```csharp
void Start()
{
    /*
    ================================
    DREAM CAR CONFIGURATOR V2.0
    Door: [Jouw naam]
    Datum: [Vandaag]
    ================================
    */

    Debug.Log("🏎️ === DREAM CAR CONFIGURATOR === 🏎️");

    // === BASISMODEL ===
    string carBrand = "Tesla"; // Pas aan naar jouw favoriete merk
    string carModel = "Model S";
    int year = 2024;

    Debug.Log("🚗 Gekozen model: " + year + " " + carBrand + " " + carModel);

    // === OPTIES MENU ===
    Debug.Log("\n🎨 === BESCHIKBARE OPTIES ===");
    Debug.Log("1. 🎨 Premium Paint (+€2,500)");
    Debug.Log("2. ⚡ Performance Upgrade (+€8,000)");
    Debug.Log("3. 🔊 Premium Audio (+€1,200)");
    Debug.Log("4. 🌟 Autopilot (+€5,000)");

    // === PRIJSBEREKENING ===
    int basePrice = 89000;
    int paintUpgrade = 2500;
    int performanceUpgrade = 8000;
    int audioUpgrade = 1200;
    int autopilotUpgrade = 5000;

    Debug.Log("\n💰 === PRIJSOVERZICHT ===");
    Debug.Log("Basisprijs: €" + basePrice);
    Debug.Log("Premium Paint: €" + paintUpgrade);
    Debug.Log("Performance: €" + performanceUpgrade);
    Debug.Log("Audio: €" + audioUpgrade);
    Debug.Log("Autopilot: €" + autopilotUpgrade);

    int totalPrice = basePrice + paintUpgrade + performanceUpgrade + audioUpgrade + autopilotUpgrade;
    Debug.Log("💸 TOTAALPRIJS: €" + totalPrice);

    // === FINANCIERING ===
    int monthlyPayment = totalPrice / 60; // 5 jaar financiering
    Debug.Log("📅 Maandelijkse betaling (60 maanden): €" + monthlyPayment);

    Debug.Log("\n🏆 Je droomauto is geconfigureerd! Start maar met sparen! 💪");
}

void Update()
{
    // Simuleer veranderende brandstofprijzen
    if (Time.frameCount % 120 == 0) // Elke 2 seconden
    {
        float fuelPrice = 1.85f + (Random.Range(-10, 10) * 0.01f);
        Debug.Log("⛽ Live brandstofprijs: €" + fuelPrice.ToString("F2") + " per liter");
    }
}
```

### ✅ Bonus Uitdagingen:

- Voeg meer auto merken en modellen toe
- Bereken CO2 uitstoot en milieu-impact
- Maak een vergelijkingstool tussen verschillende auto's
- Simuleer waardevermindering over tijd

### 🏆 Inlever Vereisten:

- Screenshot van complete configuratie
- Uitleg van hoe je variabelen hebt gebruikt (ook al leer je dit officieel later)

---

## 🎬 Oefening 5: Netflix Binge-Watch Planner ⭐⭐⭐⭐⭐

**Thema:** Streaming en Series

### 🎯 Wat Ga Je Maken?

Een geavanceerde binge-watch calculator die tijd, calorieën, snacks en meer berekent voor je serie-marathon!

### 📝 Opdracht:

1. Maak een nieuw script: `NetflixBingePlanner`
2. Combineer alles wat je hebt geleerd:

```csharp
void Start()
{
    /*
    ╔══════════════════════════════════════╗
    ║      NETFLIX BINGE-WATCH PLANNER     ║
    ║           Versie 3.0 ULTIMATE       ║
    ║      Gemaakt door: [Jouw naam]       ║
    ╚══════════════════════════════════════╝
    */

    Debug.Log("🍿 === NETFLIX BINGE-WATCH PLANNER === 📺");

    // === SERIE SELECTIE ===
    string seriesName = "Stranger Things"; // Pas aan!
    int episodesPerSeason = 8;
    int seasonCount = 4;
    int episodeDuration = 52; // minuten

    Debug.Log("🎬 Gekozen serie: " + seriesName);
    Debug.Log("📊 " + seasonCount + " seizoenen × " + episodesPerSeason + " afleveringen");

    // === TIJD BEREKENINGEN ===
    int totalEpisodes = episodesPerSeason * seasonCount;
    int totalMinutes = totalEpisodes * episodeDuration;
    int totalHours = totalMinutes / 60;
    int remainingMinutes = totalMinutes % 60; // Modulo operator!

    Debug.Log("\n⏰ === TIJD ANALYSE ===");
    Debug.Log("Totaal afleveringen: " + totalEpisodes);
    Debug.Log("Totale kijktijd: " + totalHours + " uur en " + remainingMinutes + " minuten");
    Debug.Log("Dat is " + (totalHours / 24) + " hele dagen non-stop kijken! 😱");

    // === SNACK CALCULATOR ===
    Debug.Log("\n🍿 === SNACK BEREKENINGEN ===");
    int popcornBags = totalHours / 2; // 1 zak per 2 uur
    int sodaCans = totalHours; // 1 blikje per uur
    int pizzaSlices = totalEpisodes / 3; // 1 pizza slice per 3 afleveringen

    Debug.Log("🍿 Popcorn zakken nodig: " + popcornBags);
    Debug.Log("🥤 Cola blikjes nodig: " + sodaCans);
    Debug.Log("🍕 Pizza punten nodig: " + pizzaSlices);

    // === KOSTEN BEREKENING ===
    float popcornCost = popcornBags * 2.49f;
    float sodaCost = sodaCans * 1.89f;
    float pizzaCost = pizzaSlices * 2.25f;
    float totalSnackCost = popcornCost + sodaCost + pizzaCost;

    Debug.Log("\n💰 === SNACK BUDGET ===");
    Debug.Log("Popcorn kosten: €" + popcornCost.ToString("F2"));
    Debug.Log("Cola kosten: €" + sodaCost.ToString("F2"));
    Debug.Log("Pizza kosten: €" + pizzaCost.ToString("F2"));
    Debug.Log("💸 Totale snack kosten: €" + totalSnackCost.ToString("F2"));

    // === GEZONDHEIDS WAARSCHUWING ===
    int caloriesPerHour = 350; // Gemiddeld voor snacks
    int totalCalories = totalHours * caloriesPerHour;

    Debug.Log("\n⚠️ === GEZONDHEIDS INFO ===");
    Debug.Log("Geschatte calorie-inname: " + totalCalories + " calorieën");
    Debug.Log("Dat is " + (totalCalories / 2000) + " dagen aan calorieën! 😅");

    // === PLANNING SUGGESTIES ===
    Debug.Log("\n📅 === BINGE PLANNING ===");
    Debug.Log("🎯 Optie 1: 2 uur per dag = " + (totalHours / 2) + " dagen");
    Debug.Log("🎯 Optie 2: 4 uur per dag = " + (totalHours / 4) + " dagen");
    Debug.Log("🎯 Optie 3: Weekend marathon = " + (totalHours / 16) + " weekenden");

    Debug.Log("\n🏆 Je binge-watch plan is klaar! Veel kijkplezier! 🎉");
    Debug.Log("💡 Pro tip: Vergeet niet af en toe te pauzeren voor wat beweging! 🏃‍♂️");
}

void Update()
{
    // Simuleer Netflix aanbevelingen
    if (Time.frameCount % 180 == 0) // Elke 3 seconden
    {
        string[] recommendations = {
            "Breaking Bad", "The Office", "Money Heist", "Squid Game",
            "Wednesday", "The Witcher", "Ozark", "Dark"
        };

        int randomIndex = Random.Range(0, recommendations.Length);
        Debug.Log("🔥 Netflix Aanbeveling: " + recommendations[randomIndex] + " - Nu trending!");
    }

    // Simuleer kijkvoortgang
    if (Time.frameCount % 300 == 0) // Elke 5 seconden
    {
        int watchedEpisodes = Random.Range(1, 10);
        float completionPercentage = (watchedEpisodes / 32f) * 100f; // 32 = totaal afleveringen
        Debug.Log("📈 Voortgang update: " + watchedEpisodes + " afleveringen bekeken (" +
                 completionPercentage.ToString("F1") + "% compleet)");
    }
}
```

### ✅ Bonus Uitdagingen:

- Voeg multiple series toe en vergelijk ze
- Maak een "continue watching" functie
- Bereken optimale kijktijden gebaseerd op je schema
- Voeg een rating systeem toe
- Simuleer Netflix algoritme aanbevelingen

### 🏆 Inlever Vereisten:

- Screenshot van de complete output
- Uitgebreide uitleg over welke programmeerconcepten je hebt gebruikt
- Beschrijving van je eigen aanpassingen en creativiteit

---

## 📝 Algemene Inlever Instructies

### 🎯 Voor Elke Oefening:

1. **Script file** - Upload je .cs bestand
2. **Screenshot** - Van de console output in Unity
3. **Korte beschrijving** - Wat heb je geleerd? (max 100 woorden)
4. **Github link** - Link naar je project repository

### ⭐ Bonus Punten Voor:

- Eigen creativiteit en aanpassingen
- Extra functionaliteit die niet in de opdracht stond
- Nette code met goede comments
- Experimenteren met verschillende Debug.Log() variaties

### 🏆 Success Tips:

- Begin met een oefening die past bij jouw niveau
- Experimenteer gerust met de code
- Lees de foutmeldingen - ze helpen je leren!
- Vraag hulp als je vastloopt - dat is normaal!

**🎮 Veel succes met je eerste programmeeravontuur! 🚀**
