# Game Jam Introweek 2026–2027

## "Blast Galaxy Arcade Challenge" – GD × Fullstack variant (leerjaar 2 & 3)

---

## Projectoverzicht

|                        |                                                                                    |
| ---------------------- | ---------------------------------------------------------------------------------- |
| **Periode game jam**   | Dinsdag 1 t/m donderdag 3 september 2026                                           |
| **Finale presentatie** | Vrijdag 4 september 2026 – 16:00                                                   |
| **Kickoff**            | Dinsdag 1 september – 11:15, dintelzaal                                            |
| **Opdrachtgever**      | Blast Galaxy – Arcadehal                                                           |
| **Locatie**            | School + dintelzaal (kickoff & finale)                                             |
| **Deelnemers**         | 130 studenten – Game Developer én Fullstack Developer, uitsluitend leerjaar 2 en 3 |
| **Docentenpool**       | 5 docenten / coaches                                                               |

---

[Link naar Kickoff (Miro)](https://miro.com/app/board/uXjVHHdYYoI=/?share_link_id=644464254204)

## Doelstellingen

### Inhoudelijk

- Elk team bouwt een speelbaar arcade game dat draait op **twee platforms**: de NAMCO Noir Cabinet FHD (bij Blast Galaxy) én de **eigen kast** met een **eigen zelfgebouwde controller** (op school).
- Game Developers bouwen de game in Unity; Fullstack Developers ontwerpen en bouwen de custom controller en de bijbehorende kast-opstelling (Windows 10 pc + controller).
- De game werkt op beide platforms via **Unity's New Input System** met twee control schemes.
- Tijdens de ontwikkeling werken en testen teams uitsluitend op de eigen kast-opstelling. Op donderdagmiddag installeren 2 personen per team de game bij Blast Galaxy op de NAMCO.
- De beste games, controllers én kasten worden geëxposeerd en gespeeld bij opdrachtgever Blast Galaxy.

### Didactisch en Pedagogisch

- Studenten maken kennis met medestudenten en hun studiecoach binnen een **cross-profiel** werkverband (GD ↔ Fullstack).
- Jaargrenzen vervagen: 3e jaars nemen een leidende rol; 2e jaars leveren de implementatie.
- Studenten werken met professionele workflows: GitHub, feature branches, pull requests.
- Cross-profiel samenwerking staat centraal: GD'ers en Fullstackers hebben complementaire vaardigheden en zijn van elkaar afhankelijk.
- Studenten ervaren de hectiek én het plezier van een game jam met een echt eindproduct.

---

## Opdracht – Arcade Game + Custom Controller + Eigen Kast (alle 13 teams)

Elk team bouwt **drie dingen**:

1. Een speelbaar **arcade game** dat stabiel draait op zowel de NAMCO Noir Cabinet FHD als op de eigen kast.
2. Een **eigen creatieve controller** waarmee de speler de game bestuurt.
3. Een **eigen kast-opstelling**: een Windows 10 pc met het custom input device, ingericht als complete arcade-station.

De game is via **Unity's New Input System** gebonden aan twee control schemes: `ArcadeStick` (voor de NAMCO) en `CustomDevice` (voor de eigen controller). Geen `if/else` op hardwaretype in de gameplay-code — het Input System selecteert automatisch het actieve apparaat.

---

### Deel 1 – Arcade Game

#### Hardware-specificaties NAMCO Noir Cabinet FHD (platform 1)

| Spec        | Waarde                                                                               |
| ----------- | ------------------------------------------------------------------------------------ |
| OS          | Windows 10                                                                           |
| Beeldscherm | 32" 1920×1080 (1080p)                                                                |
| Videokaart  | Nvidia GeForce GT 730 (geen zware shaders of ray tracing)                            |
| Audio       | Stereo speakers                                                                      |
| Input       | 2× 8-way joystick (digitaal), ≥4 actieknoppen + 1 startknop per speler (DirectInput) |

#### Hardware-specificaties eigen kast-opstelling (platform 2)

| Spec        | Waarde                                                                               |
| ----------- | ------------------------------------------------------------------------------------ |
| OS          | Windows 10                                                                           |
| Beeldscherm | Minimaal 1080p (team kiest zelf monitor of tv)                                       |
| Videokaart  | Moderne discrete of geïntegreerde GPU (game mag iets meer kunnen dan op de NAMCO)    |
| Audio       | Stereo speakers of losse speakers naar keuze                                         |
| Input       | Eigen zelfgebouwde controller (USB HID of Bluetooth HID), emuleert standaard gamepad |

#### Eisen aan de game

- Draait stabiel op **beide** platforms (NAMCO én eigen kast)
- Werkt met de **eigen controller** als primaire input (platform 2)
- Werkt ook volledig met de **NAMCO-joystick en knoppen** (platform 1)
- Beide inputs worden afgehandeld via **Unity's New Input System** (Input Action Asset met twee control schemes: `CustomDevice` en `ArcadeStick`)
- Speelduur per sessie: maximaal 3–5 minuten (arcade-stijl: snel, pakkend)
- Geschikt voor 1 of 2 spelers
- Visueel aantrekkelijk als promotie voor de opleiding en de arcadehal
- Bevat geluid (effecten en/of muziek)

> **Testbenadering:** de NAMCO-kast staat bij Blast Galaxy en is niet beschikbaar op school. Ontwikkel en test op de eigen kast-opstelling met een standaard USB-gamepad (HID-gamepad-bindings zijn identiek aan die van de NAMCO). De daadwerkelijke NAMCO-test vindt plaats op **donderdagmiddag bij Blast Galaxy**, wanneer 2 teamleden de game daar komen installeren.

> **Technische toelichting Unity New Input System:**
> Maak een `InputActionAsset` met twee _Control Schemes_: één voor het custom HID-device (`CustomDevice`) en één voor de NAMCO-joystick (`ArcadeStick`). Bind dezelfde acties (`Move`, `Fire`, `Start`) aan beide schemes. Het Input System selecteert automatisch het actieve apparaat op basis van het aangesloten device. Geen `if/else` op hardwaretype nodig in de gameplay-code.

#### Engine

- **Unity + New Input System** – verplicht; vereist voor de dubbele input-ondersteuning op beide platforms
- Andere engines zijn **niet** toegestaan in deze variant, zodat coaches gerichte technische begeleiding kunnen bieden en de dual-platform-integratie correct verloopt

#### Art en assets

- Mogen worden gegenereerd met AI-tools (Midjourney, DALL-E, Stable Diffusion, etc.)
- Mogen worden gedownload van rechtenvrije bronnen (itch.io, opengameart.org, freesound.org, etc.)
- Eigen gemaakte art is van harte welkom

---

### Deel 2 – Custom Controller

Bouw een **eigen creatief input device** dat de speler gebruikt om de game te besturen op de eigen kast.

#### Eisen aan de controller

- Origineel, zelfgebouwd (niet: standaard joystick of toetsenbord)
- Communiceert via USB of Bluetooth als **HID-gamepad** (zodat Unity's New Input System het automatisch herkent naast de NAMCO-joystick)
- Robuust genoeg voor gebruik door meerdere spelers tijdens de expo
- Voor de twee beste controllers: **hufterproof** voor permanente plaatsing bij Blast Galaxy
- Gedocumenteerd: schema, componentenlijst, beknopte handleiding

#### Technische richtlijnen hardware

- **Arduino Leonardo / Pro Micro**: native USB HID – emuleert een gamepad (aanbevolen) of keyboard
- **ESP32**: USB HID of Bluetooth HID
- **Raspberry Pi**: USB HID via USB-gadget-mode of Bluetooth
- **Aanbeveling**: emuleer altijd als standaard HID-gamepad (niet als keyboard), zodat het New Input System het device automatisch herkent

> Fullstack Developers zijn primair verantwoordelijk voor de controller. Zij documenteren de elektronica en firmware voor toekomstig onderhoud en de expo-documentatie.

---

### Deel 3 – Eigen Kast-opstelling (Windows 10)

Elk team richt een **eigen arcade-station** in: een pc met Windows 10 waarop de game draait via de eigen controller.

#### Minimale eisen eigen kast

- Windows 10 pc (school-pc, eigen laptop of een door school beschikbaar gesteld systeem)
- Beeldscherm aangesloten en werkend
- Eigen controller aangesloten en herkend als HID-gamepad
- Game-executable geïnstalleerd en stabiel draaiend
- De opstelling ziet er verzorgd uit voor de expo (bedrading weggewerkt, evt. kastelementen)

> De "kast" hoeft geen geschilderde houten kist te zijn — een nette tafelopstelling met monitor, pc en controller is voldoende. Teams die ambitieus zijn mogen verder gaan.

---

## Deelnemers en Teamindeling

### Overzicht deelnemers

| Klas       | Jaar | Profiel             | Aantal  |
| ---------- | ---- | ------------------- | ------- |
| sd3a       | 3    | Game Developer      | 30      |
| sd3b       | 3    | Fullstack Developer | 20      |
| sd3c       | 3    | Fullstack Developer | 20      |
| sd2a       | 2    | Game Developer      | 30      |
| sd2b       | 2    | Fullstack Developer | 30      |
| **Totaal** |      |                     | **130** |

### Teamindeling: 13 teams van ~10 studenten

#### Samenstelling per team (richtlijn)

| Rol                  | Jaar / Profiel    | Aantal per team | Taak                                                                             |
| -------------------- | ----------------- | --------------- | -------------------------------------------------------------------------------- |
| **Tech Lead**        | 3e jaar GD        | 1               | Teamleiding, game-architectuur, GitHub-structuur, PR-reviews, stand-up leiden    |
| **Senior Game Dev**  | 3e jaar GD        | 1–2             | Core gameplay, Unity New Input System, dual-platform-integratie, mentoring 2e j  |
| **Hardware Lead**    | 3e jaar Fullstack | 2–3             | Controller-ontwerp en -realisatie, HID-firmware, documentatie                    |
| **Mid Game Dev**     | 2e jaar GD        | 2–3             | Feature-implementatie, assets integreren, UI, geluid                             |
| **Mid Hardware Dev** | 2e jaar Fullstack | 2               | Controller-fabricage, installatie eigen kast, koppeling controller ↔ game testen |

> Zorg dat in elk team de GD'ers en Fullstackers actief samenwerken: de controller en de game zijn onlosmakelijk verbonden. Teams die hun disciplines te vroeg opsplitsen riskeren een niet-werkende koppeling bij de presentatie.

#### Indicatieve verdeling over teams

| Groep             | Totaal | Verdeling (13 teams)            |
| ----------------- | ------ | ------------------------------- |
| 3e jaar GD        | 30     | ~2 per team (4 teams krijgen 3) |
| 3e jaar Fullstack | 40     | ~3 per team                     |
| 2e jaar GD        | 30     | ~2 per team (4 teams krijgen 3) |
| 2e jaar Fullstack | 30     | ~2 per team (4 teams krijgen 3) |

---

## Tijdschema

### Dinsdag 1 september – Kickoffdag

| Tijd        | Activiteit                                                                                                               | Locatie              | Betrokkenen               |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ | -------------------- | ------------------------- |
| 09:00–11:00 | Kennismaking met studiecoach per klas (elke klas afzonderlijk)                                                           | Klaslokalen          | Alle studenten            |
| 11:00–11:15 | **Pauze**                                                                                                                | —                    | —                         |
| 11:15–11:45 | **Plenaire kickoff** – introductie opdracht, opdrachtgever, regels, dual-platform-toelichting                            | Dintelzaal           | Alle studenten + docenten |
| 11:45–12:15 | Teamindeling bekendmaken + GitHub repo aanmaken                                                                          | Dintelzaal / lokalen | Alle teams                |
| 12:15–13:15 | Eerste teambijeenkomst: **Design Sprint** – game-concept én controller-concept uitwerken op papier (1 geïntegreerd plan) | Lokalen/hal          | Alle teams                |
| 13:15–13:45 | **Lunch**                                                                                                                | —                    | —                         |
| 13:45–15:45 | Technische setup: Unity-project aanmaken, Input Action Asset met twee control schemes, eerste commit pushen              | Lokalen              | Alle teams                |
| 15:45–16:00 | **Pauze**                                                                                                                | —                    | —                         |
| 16:00–17:00 | Eerste implementatie starten / teamoverleg controller-ontwerp                                                            | Lokalen              | Alle teams                |

> **Pedagogische noot:** De ochtend is bewust gereserveerd voor relatieopbouw. De kracht van deze variant zit in de cross-profiel-samenwerking — coaches stimuleren GD'ers en Fullstackers om de design sprint samen te doen, niet elk apart.

---

### Woensdag 2 september – Ontwikkeldag 1

| Tijd        | Activiteit                                                                                        | Locatie      | Betrokkenen              |
| ----------- | ------------------------------------------------------------------------------------------------- | ------------ | ------------------------ |
| 09:00–09:15 | Plenaire dagopening – doelen van de dag, tips van de coaches                                      | Dintelzaal   | Alle studenten           |
| 09:15–09:30 | **Dagelijkse stand-up** per team (wat doe ik vandaag, blockers?)                                  | Lokalen      | Per team                 |
| 09:30–11:00 | **Sprint 1** – game: core gameplay; hardware: controller-prototype werkend als HID-device         | Lokalen      | Alle teams               |
| 11:00–11:15 | **Pauze**                                                                                         | —            | —                        |
| 11:15–13:15 | **Sprint 1** – vervolg                                                                            | Lokalen      | Alle teams               |
| 13:15–13:45 | **Lunch**                                                                                         | —            | —                        |
| 13:45–14:15 | **Intervisie leads** – 3e jaars tech leads + hardware leads + coaches: voortgang en knelpunten    | Apart lokaal | 3e jaars leads + coaches |
| 14:15–15:45 | **Sprint 2** – game: uitbreiding gameplay, assets; hardware: controller verfijnen, kast inrichten | Lokalen      | Alle teams               |
| 15:45–16:00 | **Pauze**                                                                                         | —            | —                        |
| 16:00–17:00 | **Sprint 2** – vervolg                                                                            | Lokalen      | Alle teams               |
| 17:00       | **Verplichte commit + push** – geen uncommitted werk einde van de dag                             | —            | Alle teams               |

---

### Donderdag 3 september – Ontwikkeldag 2 / Afrondingsdag

| Tijd        | Activiteit                                                                                                                                                                                               | Locatie               | Betrokkenen |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- | ----------- |
| 09:00–09:15 | **Stand-up** per team                                                                                                                                                                                    | Lokalen               | Per team    |
| 09:15–11:00 | **Sprint 3** – polish game, geluid, game feel, scorebord; controller robuust maken                                                                                                                       | Lokalen               | Alle teams  |
| 11:00–11:15 | **Pauze**                                                                                                                                                                                                | —                     | —           |
| 11:15–13:15 | **Sprint 3** – vervolg; volledige systeemtest op eigen kast (o.l.v. Hardware Lead); game-build klaarzetten voor NAMCO-installatie                                                                        | Lokalen               | Alle teams  |
| 13:15–13:45 | **Lunch**                                                                                                                                                                                                | —                     | —           |
| 13:45–15:15 | **Playtesting ronde** – teams spelen elkaars game op elkaars kast, feedback (2 stars + 1 wish)                                                                                                           | Lokalen / hal         | Alle teams  |
| 15:15–15:45 | Laatste aanpassingen op basis van feedback                                                                                                                                                               | Lokalen               | Alle teams  |
| 15:45–16:00 | **Code freeze** – final build op eigen kast, `git tag v1.0.0` pushen (pauze = geen nieuwe code)                                                                                                          | Lokalen               | Alle teams  |
| 16:00–17:30 | **Per team 2 personen** (Tech Lead + Hardware Lead) naar **Blast Galaxy** voor installatie en test op NAMCO-kast; overige teamleden: voorbereiding presentatie + eerste opbouw expo-opstelling op school | Blast Galaxy / school | Alle teams  |

---

### Vrijdag 4 september – Finaledag & Presentatie

| Tijd        | Activiteit                                                                                                                   | Locatie    | Betrokkenen            |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------------------- |
| 09:00–11:00 | Opbouw expo: eigen kasten opstellen en testen, controller aansluiten en verifiëren (NAMCO al geïnstalleerd bij Blast Galaxy) | Dintelzaal | Alle teams             |
| 11:00–11:15 | **Pauze**                                                                                                                    | —          | —                      |
| 11:15–13:15 | **Interne jury-ronde** – docenten spelen alle games op de eigen kast-opstellingen, shortlist beste spellen en controllers    | Dintelzaal | Docenten               |
| 13:15–13:45 | **Lunch**                                                                                                                    | —          | —                      |
| 13:45–15:45 | Teams staan bij hun opstelling – jury en klant lopen rond, pitches per team (3 min per team)                                 | Dintelzaal | Alle teams + klant     |
| 15:45–16:00 | **Pauze**                                                                                                                    | —          | —                      |
| **16:00**   | **Plenaire finale** – opdrachtgever Blast Galaxy houdt toespraak, aankondiging winnende games, beste controllers en kasten   | Dintelzaal | Alle studenten + klant |
| 16:30–17:00 | **Prijsuitreiking** + afsluiting introweek                                                                                   | Dintelzaal | Alle aanwezigen        |

---

## Rollen en Verantwoordelijkheden

### 3e jaars GD – Tech Lead / Scrum Master

- Neemt eindverantwoordelijkheid voor het team
- Stelt de GitHub-structuur op (repo, branch-strategie, PR-template)
- Bewaakt de voortgang en lost technische game-blockers op
- Begeleidt 2e jaars GD bij technische vragen (**coachend, niet overnemend**)
- Leidt de dagelijkse stand-up
- Beoordeelt en merget pull requests
- Is het eerste aanspreekpunt voor de docent

### 3e jaars Fullstack – Hardware Lead

- Neemt de verantwoordelijkheid voor het controller-ontwerp en de kast-opstelling
- Ontwerpt het elektronica-schema en kiest componenten
- Begeleidt 2e jaars Fullstack bij de hardware-implementatie
- Garandeert dat de controller als stabiele HID-gamepad wordt herkend vóór einde dag 1
- Documenteert schema, componentenlijst en handleiding
- Coördineert de koppeling controller ↔ Unity New Input System met de Tech Lead

### 2e jaars GD – Mid Game Developer

- Werkt aan feature-implementatie, assets, UI en geluid in Unity
- Draagt bij aan code reviews via pull requests
- Test de game op beide platforms (NAMCO én eigen kast)

### 2e jaars Fullstack – Mid Hardware Developer

- Bouwt de controller fysiek (solderen, bedrading, behuizing)
- Installeert en configureert de eigen kast-opstelling (pc, monitor, controller)
- Test de HID-koppeling op de Windows 10 eigen kast en rapporteert bevindingen aan de Hardware Lead

---

## Docentenbegeleiding

### Taakverdeling binnen het docententeam (5 coaches)

| Rol                    | Aantal docenten | Taken                                                                                                                     |
| ---------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **Projectcoördinator** | 1               | Eindverantwoordelijke programma, contactpersoon Blast Galaxy, logistiek NAMCO-kasten en expo, GitHub-organisatie aanmaken |
| **Hardware coach**     | 2               | Hardware-aanspreekpunt voor alle teams; rondes langs alle teams voor hardware-check; elk ook 3–4 teams als primaire coach |
| **Team coach**         | 2               | Elk 4–5 teams begeleiden op game-voortgang én cross-profiel-samenwerking                                                  |

### Verdeling coaches over teams (indicatief)

| Coach                   | Primaire teams egeleiding | Specialisme (aanspreekpunt alle teams) |
| ----------------------- | ------------------------- | -------------------------------------- |
| Coach 1 (Projectcoörd.) | Teams 1, 2                | Coördinatie en planning                |
| Coaches 2,3 (Hardware)  | Teams 3, 4, 5, 6, 7       | Hardware en electronica                |
| Coaches 4,5 (Gamedev)   | Teams 8, 9, 10, 11, 12    | Unity Gamedev                          |

### Dagelijkse coachingtaken

**Elke dag:**

- Bijwonen van de stand-up van eigen teams (~10 min per team)
- Signaleren van cross-profiel spanningen: werken GD'ers en Fullstackers écht samen?
- Voortgangsbewaking via GitHub (commits, PR-activiteit bekijken)
- Scopen bewaken: is de game haalbaar? Is de controller op tijd werkend als HID-device?
- Hardware coaches lopen dagelijks alle 13 teams langs voor een korte hardware-check (~5 min per team)

**Coachende houding (pedagogy):**

> Stel vragen in plaats van antwoorden te geven. Geef 3e jaars de ruimte om te leiden, maar grijp in bij stagnatie of conflict. Controleer actief of de Fullstack-studenten en GD-studenten niet in gescheiden bubbels werken.

**Woensdagmiddag intervisie (13:45–14:15):**

- Coaches + 3e jaars tech leads en hardware leads komen samen in apart lokaal
- Doel: signaleren van knelpunten, wederzijdse ondersteuning, scope-adjustments
- Coaches bespreken kort de staat van hun teams (stoplicht-methode: groen/oranje/rood)
- Specifiek aandachtspunt: is de controller-game-koppeling gevalideerd (dual-platform werkt)?

---

## GitHub Workflow

Alle teams werken **verplicht** met GitHub. De 3e jaars Tech Lead zet de repository op.

### Vereisten

1. **Één repository per team**
   - Naam: `gamejam-2627-gd-fs-team-XX` (XX = teamnummer)
   - Onder de GitHub-organisatie: `SoftwareDev-GameJam-2627`

2. **Branch-strategie:**
   - `main` – stabiele, werkende versie (alleen via PR's)
   - `develop` – integratiebranch
   - `feature/naam-van-feature` – per feature een eigen branch

3. **Pull requests:**
   - Elke feature wordt via een PR gemerged in `develop`
   - PR vereist minimaal 1 review (bij voorkeur van de Tech Lead of Hardware Lead)
   - PR-beschrijving bevat: wat is er gebouwd + hoe te testen

4. **Commitberichten:**
   - Zinvolle, beschrijvende berichten (in het Nederlands of Engels)
   - Geen commits rechtstreeks op `main` of `develop`

5. **Verplichte tags:**
   - `v0.1` – na einde dag 1 (eerste werkende versie, ook al is het minimaal)
   - `v1.0.0` – bij code freeze op donderdag 15:45

### Minimale GitHub-activiteit per persoon

- Minimaal 1 eigen feature branch aangemaakt en gebruikt
- Minimaal 2 commits met beschrijvende berichten
- Minimaal 1 pull request ingediend en goedgekeurd

---

## Beoordelingscriteria

> De game jam wordt **niet beoordeeld met een studiecijfer**. Het doel is leren, samenwerken en een product presenteren aan een echte opdrachtgever. De jury (coaches + Blast Galaxy) gebruikt onderstaande criteria voor de prijsuitreiking.

### Jury-criteria – alle teams (game + controller + kast)

**Game:**

| Criterium                    | Toelichting                                                |
| ---------------------------- | ---------------------------------------------------------- |
| **Speelbaarheid**            | Is de game leuk en vlot speelbaar?                         |
| **Arcade-gevoel**            | Past het bij de sfeer en het tempo van een arcadehal?      |
| **Technische uitvoering**    | Draait het stabiel op zowel de NAMCO als de eigen kast?    |
| **Creativiteit**             | Origineel concept of een unieke twist op een bekend genre? |
| **Presentatiewaarde**        | Trekken de visuals/audio aandacht in een drukke ruimte?    |
| **Professionaliteit GitHub** | Actief gebruik van branches en PR's zichtbaar in de repo?  |

**Controller:**

| Criterium                 | Toelichting                                                   |
| ------------------------- | ------------------------------------------------------------- |
| **Originaliteit**         | Hoe creatief en uniek is het input device?                    |
| **Technische integratie** | Werkt de koppeling controller ↔ game stabiel en responsief?   |
| **Robuustheid**           | Is het stevig genoeg voor gebruik door meerdere spelers?      |
| **Game-controller fit**   | Is de game specifiek ontworpen rondom het input device?       |
| **Documentatie**          | Is de technische opbouw gedocumenteerd (schema, handleiding)? |

**Kast-opstelling:**

| Criterium         | Toelichting                                                        |
| ----------------- | ------------------------------------------------------------------ |
| **Afwerking**     | Is de opstelling verzorgd en presentabel voor de expo?             |
| **Stabiliteit**   | Blijft de hele setup (pc + controller + game) stabiel staan?       |
| **Originaliteit** | Heeft het team extra moeite gedaan aan de presentatie van de kast? |

---

## Prijzen en Afsluiting

### Prijzen

| Prijs                              | Omschrijving                                                                                                  |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Beste game overall**             | Vrijkaartjes voor Blast Galaxy voor het volledige team                                                        |
| **Beste 3 games + controllers**    | Worden geïnstalleerd op de NAMCO Noir Cabinet FHD en tentoongesteld bij Blast Galaxy                          |
| **Beste custom controller + kast** | De beste 2 controllers + kast-opstellingen komen permanent bij Blast Galaxy te staan (na hufterproof-keuring) |
| **Eervolle vermeldingen**          | Naar inzicht jury: meest origineel concept, beste cross-profiel-samenwerking, meest ambitieus, etc.           |

### Presentatieformat (vrijdag 16:00)

- Elk team staat bij zijn eigen kast-opstelling én bij de NAMCO (expo-format)
- Jury en opdrachtgever lopen rond; elk team geeft een **pitch van 3 minuten** (game + controller + kast uitleggen)
- Aansluitend toespraak opdrachtgever Blast Galaxy en aankondiging van de winnaars

---

## Didactische en Pedagogische Richtlijnen

### Leerprincipes

#### 1. Cross-profiel samenwerking als kernleerdoel

Game Developers en Fullstack Developers hebben in deze variant complementaire, wederzijds afhankelijke rollen. GD'ers kunnen geen werkende koppeling bouwen zonder de controller van de Fullstackers; Fullstackers hebben geen zinvol device zonder de game van de GD'ers. Coaches stimuleren dat dit bewustzijn er is vanaf dag 1.

#### 2. Near-peer learning (peer-coaching)

3e jaars leren door te begeleiden; 2e jaars leren van studenten die dezelfde stof recent zelf hebben doorgemaakt. Zonder 1e jaars liggen de verwachtingen hoger: het eindproduct moet zichtbaar afgebakender en professioneler zijn.

#### 3. Project Based Learning (PBL)

De game jam is een authentieke, tijdgebonden opdracht met een echte opdrachtgever en echte stakes (de controller én kast kunnen permanent bij Blast Galaxy komen te staan). Dit verhoogt intrinsieke motivatie aanzienlijk.

#### 4. Constructivisme (learning by doing)

Studenten leren door te bouwen, te falen, te herstellen en te itereren. Coaches creëren de leeromgeving en stellen de kaders — studenten bouwen de oplossing.

#### 5. Motivatie vanuit zelfbeschikking

- **Autonomie**: Teams bepalen zelf hun game-concept, controller-ontwerp en kast-presentatie.
- **Competentie**: Duidelijke, haalbare deliverables per sprint; stretch-goals voor ambitieuze teams.
- **Verbondenheid**: Cross-profiel eigenaarschap van het eindproduct — GD'ers en Fullstackers zijn samen trots op het geheel.

---

### Pedagogische aandachtspunten per fase

#### Dag 1 ochtend – Relatieopbouw als fundament

De ochtend van dag 1 is cruciaal. Studenten zijn gewend aan hun eigen profiel-bubbel. Neem ruim de tijd voor:

- Kennismaking: wie zit in het team, welk profiel, welk jaar, wat kunnen ze?
- Bespreek het programma van de introweek open en eerlijk
- Creëer een veilige sfeer: fouten maken is onderdeel van leren

> Een goede relatie met de studiecoach en teamgenoten van een ander profiel legt de basis voor productieve cross-disciplinaire samenwerking.

#### Voorkomen van profiel-eilanden

Het grootste risico in deze variant: GD'ers bouwen de game, Fullstackers bouwen de controller — en ze praten te weinig met elkaar. Coaches letten actief op:

- Doen GD'ers en Fullstackers de design sprint écht samen?
- Is de controller-game-koppeling een gedeelde verantwoordelijkheid?
- Testen GD'ers de game actief met de controller van de Fullstackers (en andersom)?

Interventiestrategie: vraag in de stand-up: _"Hoe heb jij gisteren samengewerkt met iemand van een ander profiel?"_

#### Feedback-cultuur opbouwen

- Leer teams constructief feedback geven: **2 stars + 1 wish**
- Coaches modellen dit gedrag tijdens check-ins en de playtesting-ronde
- Voorkom publieke afrekening; geef feedback altijd respectvol

#### Omgaan met stagnatie

| Signaal                                        | Oorzaak                             | Interventie                                                        |
| ---------------------------------------------- | ----------------------------------- | ------------------------------------------------------------------ |
| Controller werkt niet als HID-device           | Firmware-fout of verkeerde USB-mode | Hardware coach ter plekke; fallback: keyboard-emulatie via Arduino |
| Game werkt niet met controller                 | Verkeerd control scheme in Unity    | Senior GD + Hardware Lead samen: valideer Input Action Asset       |
| GD en Fullstack werken volledig los van elkaar | Gebrek aan gedeeld begrip           | Coaches: forceer gezamenlijke integratiesessie                     |
| Team bouwt maar voegt niks speelbaars toe      | Te ambitieus concept                | Scope reduceren met Tech Lead: definieer MVP opnieuw               |
| 3e jaars doet alles zelf                       | Dominantie / gebrek aan vertrouwen  | Gesprek apart: hoe begeleid je ipv overnemen?                      |
| Conflict in team                               | Stijlverschillen, druk              | Mediationgesprek door coach; separeer indien nodig                 |
| Team haalt code freeze niet                    | Te late start, scope creep          | Eerder ingrijpen; freeze desnoods per team flexibiliseren          |

#### Scope management

- Coaches helpen bij het definiëren van een **MVP** op dag 1 avond
- Vuistregel game: _"Wat is het kleinste, complete spelletje dat je in 2 dagen kunt bouwen?"_
- Vuistregel controller: _"Welk device kun je in een halve dag werkend krijgen als HID-gamepad?"_ — twee knoppen en een joystick is een prima start
- Vuistregel kast: _"Een nette tafelopstelling met pc, monitor en controller is al een kast"_
- Een werkend eenvoudig spel met een simpele controller is altijd beter dan een halfgebouwde ambitieuze game zonder werkende input

---

## Praktische Voorbereiding

### Checklist vóór 1 september

**Projectcoördinator:**

- [ ] Contact met Blast Galaxy: bevestig aanwezigheid vrijdag 16:00, inventariseer eventuele wensen
- [ ] Afstemmen met Blast Galaxy: NAMCO beschikbaar op **donderdagmiddag 16:00–17:30** voor installatie door student-delegaties (26 studenten, verspreid over 13 teams)
- [ ] Windows 10 pc's beschikbaar voor de eigen kast-opstellingen (of inventariseer welke teams eigen hardware meenemen)
- [ ] Lokalen gereserveerd voor alle 13 teams (of open werkruimtes)
- [ ] GitHub-organisatie aangemaakt: `SoftwareDev-GameJam-2627`
- [ ] Teamindelingslijst definitief (wie zit in welk team, teamnummers, profielmix per team)
- [ ] Kickoff-presentatie voorbereid (inclusief dual-platform-toelichting, beelden van Blast Galaxy)
- [ ] Informatiebrief aan studenten verstuurd vóór introweek (zie hieronder)

**Hardware coaches (Coach 2 + 3):**

- [ ] Arduino Leonardo / Pro Micro boards – minimaal 2 per team = 26 stuks (+ reserve)
- [ ] ESP32 boards als alternatief / backup – minimaal 10 stuks
- [ ] Elektronica basissets per team: knoppen, joystick-modules, bedrading, connectoren, breadboards (13 sets)
- [ ] Gedeeld gereedschap: soldeerbouts (minimaal 4), multimeters, kniptangen, schroevendraaiers
- [ ] Inventariseer vooraf per team welke Fullstack-studenten elektronica-ervaring hebben
- [ ] Schrijf een korte hardware-quickstart (1 A4) met Arduino HID-gamepad-voorbeeldcode, te delen op dag 1

**Alle coaches:**

- [ ] Teamindelingslijst doornemen: ken je eigen teams en de profielmix
- [ ] Unity-projecttemplate klaar: leeg project met Input Action Asset (`ArcadeStick` + `CustomDevice` control schemes) en USB-gamepad-bindings
- [ ] Mini Git-workshop materiaal niet nodig (alle deelnemers hebben al Git-ervaring)
- [ ] Standaard USB-gamepads beschikbaar voor ontwikkeling op school (zodat GD'ers de input kunnen testen vóór de controller klaar is)

---

### Informatiebrief aan studenten (vóór introweek)

Studenten ontvangen uiterlijk **vrijdag 28 augustus** de volgende informatie:

1. **Wat is de game jam?** – korte omschrijving van het programma en de opdrachtgever
2. **Technische installatielijst** – Unity (LTS-versie) + New Input System package installeren, GitHub-account controleren
3. **Teamindeling** – wie zit in jouw team, welk profiel en jaar (of: dit wordt bekendgemaakt op dag 1)
4. **Wat meenemen?** – laptop, oplader, eventuele eigen hardware-componenten of gereedschap; ideeën voor een creatieve controller
5. **Verwachting** – dit is geen 1e-jaars gamejam; de verwachting is een volledig werkend product op twee platforms aan het einde van de week

---

### Benodigde materialen en middelen

| Item                              | Aantal               | Verantwoordelijke                 |
| --------------------------------- | -------------------- | --------------------------------- |
| NAMCO Noir Cabinet FHD            | 1 (bij Blast Galaxy) | Blast Galaxy / Projectcoördinator |
| Windows 10 pc's voor eigen kasten | 13                   | IT-beheer / coörd.                |
| Monitoren voor eigen kasten       | 13                   | IT-beheer / coörd.                |
| Arduino/ESP32 kits (per team)     | 13 sets              | Hardware coaches                  |
| Elektronica gereedschap           | 4 sets gedeeld       | Hardware coaches                  |
| Soldeerbouts                      | 4+                   | Hardware coaches                  |
| USB-gamepads (voor ontwikkeling)  | 13+                  | Coaches / IT-beheer               |
| Laptops / werkstations            | Per student          | IT-beheer                         |
| Dintelzaal (kickoff + finale)     | Dag 1 + dag 4        | Projectcoördinator                |
| Lokalen (13 teams)                | Dag 1 t/m 4          | Projectcoördinator                |
| GitHub org + 13 repos             | 13                   | Projectcoördinator                |
| Teamkaarten (print, A5)           | 13                   | Projectcoördinator                |
| Beamer / scherm in dintelzaal     | 1                    | IT-beheer / coörd.                |

---

## Risico's en Mitigatie

| Risico                                                     | Kans   | Impact | Mitigatie                                                                                               |
| ---------------------------------------------------------- | ------ | ------ | ------------------------------------------------------------------------------------------------------- |
| GD en Fullstack werken in gescheiden bubbels               | Hoog   | Hoog   | Coach monitort actief; verplichte integratiesessie aan einde dag 1                                      |
| Controller werkt niet als HID-gamepad                      | Midden | Hoog   | Hardware coaches paraat; fallback: keyboard-emulatie via Arduino Leonardo                               |
| Game werkt niet met custom device (Unity-koppeling)        | Midden | Hoog   | Unity-template met werkend dual-scheme-voorbeeld meeleveren; Tech Lead + Hardware Lead verantwoordelijk |
| Te ambitieuze scope; game of controller onafgemaakt        | Hoog   | Hoog   | Coach helpt bij MVP-definitie einde dag 1; dagelijkse scope-check                                       |
| NAMCO niet beschikbaar op donderdagmiddag bij Blast Galaxy | Laag   | Midden | Tijdig afstemmen met Blast Galaxy; alternatief: installatie vrijdagochtend vroeg                        |
| Windows 10 pc voor eigen kast niet beschikbaar             | Laag   | Midden | Inventariseer vooraf; studenten mogen eigen laptop gebruiken als eigen kast                             |
| 3e jaars domineren; 2e jaars haken af                      | Midden | Midden | Coach monitort actief; check-in met 2e jaars apart op dag 2                                             |
| Conflict in team (cross-profiel friction)                  | Midden | Midden | Mediationgesprek door coach; wijst op gedeelde eindverantwoordelijkheid                                 |
| Klant (Blast Galaxy) afwezig op vrijdag                    | Laag   | Hoog   | Tijdig bevestigen; backup: presentatie opnemen/streamen                                                 |

---

_Plan opgesteld: juni 2026 | Versie 1.0 | Opleiding Software Developer – GD × Fullstack variant (leerjaar 2 & 3)_

_[Kickoff link](https://miro.com/app/board/uXjVHHdYYoI=/?share_link_id=644464254204)_
