# Oefeningen Les 1.2: Introductie Scripting in C#

## Overzicht Oefeningen

Kies **minimaal 1 oefening** die past bij jouw niveau en interesse.

### Niveaus:

- ⭐ **Beginner** - Je eerste keer programmeren
  - [Oefening 1B: Spotify Playlist Generator](#Oefening-1B:-Spotify-Playlist-Generator)
  - [Oefening 2B: Instagram Story Creator]
  - [Oefening 3B: Minecraft Crafting Recipe]
- ⭐⭐ **Starter** - Je begrijpt de basis al een beetje
- ⭐⭐⭐ **Gevorderd** - Je wilt meer uitdaging

---

## Algemene Inlever Instructies

### Voor Elke Oefening:

1. **Script file** - Upload je .cs bestand naar GitHub
2. **README documentatie** - Verwerk je opdracht in je README met titel, beschrijving, gif en code link
3. **GitHub repository** - Zorg dat je project beschikbaar is op GitHub en dat je de link naar je readme hebt ingeleverd op simulise.

### Success Tips:

- Begin met een oefening die past bij jouw niveau en interesse
- Experimenteer gerust met de code
- Lees de foutmeldingen - ze helpen je leren!
- Vraag hulp als je vastloopt - dat is normaal!

---

## Oefening 1B: Spotify Playlist Generator ⭐

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

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Oefening 2B: Instagram Story Creator ⭐

**Thema:** Social Media en Content Creation

### Wat Ga Je Maken?

Een script dat jouw perfecte Instagram story post samenstelt, compleet met hashtags en locatie!

### Opdracht:

1. Maak een nieuw script: `InstagramStory`
2. In de `Start()` functie, maak je story:

```csharp
void Start()
{
    // Je story post
    Debug.Log("=== NIEUWE INSTAGRAM STORY ===");
    Debug.Log("Foto: [Beschrijf je foto, bijv: Zonsondergang op het strand]");
    Debug.Log("Caption: [Jouw leuke tekst]");

    // Locatie en tijd
    Debug.Log("Locatie: [Jouw stad/favoriete plek]");
    Debug.Log("Gepost om: 18:30");

    // Hashtags
    Debug.Log("#photography #sunset #amazing #nofilter #life");

    Debug.Log("Story succesvol gepost! Wacht op de likes...");
}
```

### Toevoegingen aan de code:

- Voeg meer hashtags toe die bij jou passen
- Maak een tweede story post over iets anders
- Tel hoeveel karakters je caption heeft (tip: tel de letters!)

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Oefening 3B: Minecraft Crafting Recipe ⭐

**Thema:** Gaming en Crafting

### Wat Ga Je Maken?

Een script dat je laat zien hoe je jouw favoriete Minecraft item craft, stap voor stap!

### Opdracht:

1. Maak een nieuw script: `MinecraftCrafting`
2. In de `Start()` functie, toon je crafting recipe:

```csharp
void Start()
{
    // Welkom bericht
    Debug.Log("=== MINECRAFT CRAFTING GUIDE ===");
    Debug.Log("Vandaag maken we: Diamond Sword!");

    // Benodigde materialen
    Debug.Log("=== MATERIALEN NODIG ===");
    Debug.Log("2x Diamond");
    Debug.Log("1x Stick");

    // Crafting steps
    Debug.Log("=== CRAFTING STAPPEN ===");
    Debug.Log("Stap 1: Open je crafting table");
    Debug.Log("Stap 2: Plaats diamond in het midden-boven vakje");
    Debug.Log("Stap 3: Plaats diamond in het midden vakje");
    Debug.Log("Stap 4: Plaats stick in het midden-onder vakje");

    Debug.Log("Diamond Sword gecrafted! Nu kun je monsters verslaan!");
}
```

### Toevoegingen aan de code:

- Kies een ander Minecraft item om te craften
- Voeg de durability (hoe lang het item meegaat) toe
- Maak een lijst van wat je met het item kunt doen

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Oefening 4S: YouTube Channel Stats ⭐⭐

**Thema:** Content Creation en Influencers

### Wat Ga Je Maken?

Een script dat de statistieken van jouw droomkanaal toont, inclusief simpele berekeningen!

### Opdracht:

1. Maak een nieuw script: `YouTubeChannelStats`
2. Gebruik basale rekenkunde in je berichten:

```csharp
void Start()
{
    // === KANAAL INFO ===
    Debug.Log("=== YOUTUBE KANAAL DASHBOARD ===");
    Debug.Log("Kanaal: [Jouw kanaal naam]");
    Debug.Log("Content Creator: [Jouw naam]");

    // === STATISTIEKEN ===
    Debug.Log("=== HUIDIGE STATS ===");
    Debug.Log("Subscribers: " + 15420);
    Debug.Log("Total views: " + 2847362);
    Debug.Log("Uploaded videos: " + 127);

    // === BEREKENINGEN ===
    Debug.Log("=== INTERESSANTE CIJFERS ===");
    Debug.Log("Gemiddelde views per video: " + (2847362 / 127));
    Debug.Log("Geschatte maandelijkse inkomsten: €" + (15420 / 1000 * 3));
    Debug.Log("Views per subscriber: " + (2847362 / 15420));

    // === DOELEN ===
    Debug.Log("=== VOLGENDE DOELEN ===");
    Debug.Log("Doel 1: " + 20000 + " subscribers");
    Debug.Log("Doel 2: " + 3000000 + " total views");
    Debug.Log("Nog " + (20000 - 15420) + " subscribers te gaan!");

    Debug.Log("Keep creating awesome content!");
}
```

### Toevoegingen aan de code:

- Voeg meer statistieken toe (likes, comments, dislikes)
- Bereken hoeveel subscribers je per maand erbij krijgt
- Maak verschillende video categorieën met eigen stats

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Oefening 5S: TikTok Viral Calculator ⭐⭐

**Thema:** Korte Video Content en Trends

### Wat Ga Je Maken?

Een script dat berekent hoe viral jouw TikTok video kan gaan, met trending hashtags en statistieken!

### Opdracht:

1. Maak een nieuw script: `TikTokViralCalculator`
2. Gebruik comments om je code netjes te organiseren:

```csharp
void Start()
{
    /*
    ===============================
    TIKTOK VIRAL CALCULATOR V1.0
    Gemaakt door: [Jouw naam]
    ===============================
    */

    Debug.Log("=== TIKTOK VIRAL CALCULATOR ===");

    // === VIDEO INFO ===
    Debug.Log("Video titel: [Jouw video idee]");
    Debug.Log("Video lengte: 45 seconden");
    Debug.Log("Trending sound: GEBRUIKT");

    // === VERWACHTE STATS ===
    Debug.Log("=== VIRAL VOORSPELLING ===");
    int expectedViews = 125000;
    int expectedLikes = expectedViews / 10; // 10% like ratio
    int expectedShares = expectedViews / 50; // 2% share ratio
    int expectedComments = expectedViews / 100; // 1% comment ratio

    Debug.Log("Verwachte views: " + expectedViews);
    Debug.Log("Verwachte likes: " + expectedLikes);
    Debug.Log("Verwachte shares: " + expectedShares);
    Debug.Log("Verwachte comments: " + expectedComments);

    // === HASHTAG STRATEGIE ===
    Debug.Log("=== TRENDING HASHTAGS ===");
    Debug.Log("#fyp #viral #trending #funny #relatable");
    Debug.Log("#tiktokmademe #foryoupage #vibes #mood");

    // === UPLOAD TIMING ===
    Debug.Log("=== BESTE UPLOAD TIJDEN ===");
    Debug.Log("Ochtend: 9:00 - Engagement: 65%");
    Debug.Log("Avond: 19:00 - Engagement: 85%");
    Debug.Log("Nacht: 22:00 - Engagement: 90%");

    // === SUCCESS KANS ===
    int successScore = 75; // Gebaseerd op trending sound + goede hashtags
    Debug.Log("=== VIRAL SUCCESS KANS ===");
    Debug.Log("Success Score: " + successScore + "/100");
    Debug.Log("Kans op viral: " + (successScore > 70 ? "HOOG" : "GEMIDDELD"));

    Debug.Log("Ready to go viral? Post je video!");
}
```

### Toevoegingen aan de code:

- Voeg verschillende video categorieën toe (dans, comedy, educational)
- Bereken potentiële follower groei na viral video
- Maak een vergelijking tussen verschillende upload tijden

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Oefening 6S: Gaming Setup Configurator ⭐⭐

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

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)

---

## Oefening 7G: Social Media Dashboard ⭐⭐⭐

**Thema:** Social Media en Influencers

### Wat Ga Je Maken?

Een dashboard dat verschillende social media statistieken toont, met realtime updates in de Update functie!

### Opdracht:

1. Maak een nieuw script: `SocialMediaDashboard`
2. Gebruik zowel `Start()` als `Update()`:

```csharp
void Start()
{
    // === ACCOUNT SETUP ===
    Debug.Log("Social Media Dashboard Gestart!");
    Debug.Log("Account: @[jouw_username]");
    Debug.Log("Dashboard geladen...");

    // === STATISTIEKEN ===
    Debug.Log("Instagram followers: " + 1247);
    Debug.Log("Twitter followers: " + 892);
    Debug.Log("YouTube subscribers: " + 15600);
    Debug.Log("TikTok followers: " + 3421);

    // === RECENT ACTIVITEIT ===
    Debug.Log("Laatste post: 23 likes in 5 minuten!");
    Debug.Log("Nieuwe comments: 7");
}
private float time = 0f;
void Update()
{
    // Deze code toont live updates (elke seconde ongeveer)
    // LET OP: Dit maakt veel berichten! Test maar kort.
    time += Time.deltaTime;
    // Toon elke seconde een live update
    if (time >= 1f)
    {
        time = 0f;
        Debug.Log("Live update - Frame: " + Time.frameCount + " | Online gebruikers: " + Random.Range(100, 500));
    }
}
```

### Toevoegingen aan de code:

- Voeg meer social media platforms toe
- Simuleer follower groei over tijd
- Maak verschillende soorten posts (foto/video/story)

### Inlever Vereisten:

Verwerk je opdracht in je README. Deze bevat de titel van de opdracht, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[Zie voorbeeld format](../README.md#Voorbeeld-README-Opdracht-Format)
