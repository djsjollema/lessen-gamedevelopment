# Verdiepende Programmeeropdrachten M4 - Unity & C#

Hieronder vind je 20 extra programmeeropdrachten voor studenten die sneller door het basisprogramma heen zijn. Elke opdracht duurt ongeveer 2 uur en verdiept of verbreedt de kennis binnen Unity en C#. Elke opdracht bevat een omschrijving, leerdoelen, een talig stappenplan en hints voor zelfstandig onderzoek.

---

## 1. Power-Up Systeem

**Omschrijving:**  
Laat de speler een power-up oppakken die tijdelijk een effect geeft, zoals sneller bewegen. Na 5 seconden verdwijnt het effect automatisch.

**Leerdoelen:**

- Triggers en tags gebruiken
- Tijdelijke effecten aansturen
- Coroutines begrijpen

**Stappenplan + Hints:**

1. Kies een object in je scène dat als power-up dient _(Hint: "Unity prefab object maken")_
2. Herken het object in je script _(Hint: "Unity object tag gebruiken")_
3. Bedenk wat er gebeurt bij aanraking _(Hint: "Unity OnTriggerEnter gebruiken")_
4. Ontwerp het tijdelijke effect _(Hint: "Unity variable aanpassen tijdens collision")_
5. Laat het effect na 5 seconden stoppen _(Hint: "Unity Coroutine WaitForSeconds")_
6. Verwijder het power-up object na gebruik _(Hint: "Unity Destroy gameObject")_

---

## 2. AI Patrol System

**Omschrijving:**  
Laat een vijand automatisch bewegen tussen meerdere punten.

**Leerdoelen:**

- Waypoints gebruiken
- Vector-afstanden meten
- Herhalende beweging maken

**Stappenplan + Hints:**

1. Zet meerdere waypoints in je scène _(Hint: "Unity waypoint systeem maken")_
2. Kies steeds een doelpunt _(Hint: "Unity array van waypoints gebruiken")_
3. Meet de afstand tot het doel _(Hint: "Unity Vector3.Distance uitleg")_
4. Wissel van waypoint bij aankomst _(Hint: "Unity loop door array met index")_
5. Laat dit gedrag blijven herhalen _(Hint: "Unity Update functie gebruiken")_

---

## 3. Countdown Timer + Game Over

**Omschrijving:**  
Laat een timer aftellen en laad een Game Over-scherm als de tijd op is.

**Leerdoelen:**

- Tijd meten met deltaTime
- UI dynamisch bijwerken
- Scene transitions uitvoeren

**Stappenplan + Hints:**

1. Stel de begintijd van het level in _(Hint: "Unity float timer aanmaken")_
2. Laat de tijd omlaag gaan _(Hint: "Unity Time.deltaTime")_
3. Toon de resterende tijd op het scherm _(Hint: "Unity TextMeshPro tijd weergeven")_
4. Controleer wanneer de tijd op is _(Hint: "Unity if statement vergelijken met 0")_
5. Schakel dan over naar een Game Over scene _(Hint: "Unity SceneManager.LoadScene")_

---

## 4. Besturingsmodi Wisselen

**Omschrijving:**  
Laat de speler wisselen tussen lopen en rijden met verschillende besturing.

**Leerdoelen:**

- Boolean toestand wisselen
- Meerdere bewegingsvormen beheren
- Inputcondities toepassen

**Stappenplan + Hints:**

1. Beschrijf beide modi _(Hint: "Unity player movement ideeën")_
2. Sla op in welke modus je zit _(Hint: "Unity boolean toggle")_
3. Voeg een toets toe om te wisselen _(Hint: "Unity Input.GetKeyDown voorbeeld")_
4. Pas beweging aan op basis van modus _(Hint: "Unity if-statement per movement")_
5. Test of de wissel goed werkt _(Hint: "Unity debuggen inputmodi")_

---

## 5. Inventaris met Dictionary

**Omschrijving:**  
Laat de speler meerdere objecten verzamelen en bijhouden hoeveel er van elk is.

**Leerdoelen:**

- Dictionaries toepassen
- UI updaten via code
- Triggers gebruiken

**Stappenplan + Hints:**

1. Bepaal welke items verzameld kunnen worden _(Hint: "Unity collectable prefab")_
2. Herken items via tag of naam _(Hint: "Unity object tag gebruiken")_
3. Houd aantallen bij in een dictionary _(Hint: "C# Dictionary beginnersuitleg")_
4. Update de UI per item _(Hint: "Unity TextMeshPro bijwerken via script")_
5. Zorg dat het werkt met meerdere gelijktijdige pickups _(Hint: "Unity meerdere pickups detecteren")_

---

## 6. Target Practice Minigame

**Omschrijving:**  
Laat doelen verschijnen die de speler moet raken voor punten.

**Leerdoelen:**

- Prefabs spawnen op random posities
- Interactie + score bijhouden
- UI feedback geven

**Stappenplan + Hints:**

1. Laat doelen op random plekken spawnen _(Hint: "Unity Random position object spawn")_
2. Detecteer wanneer ze geraakt worden _(Hint: "Unity object klikken detecteren")_
3. Tel score bij elke hit _(Hint: "Unity score variabele bijhouden")_
4. Verwijder doelen na een hit _(Hint: "Unity Destroy object")_
5. Laat score op het scherm zien _(Hint: "Unity TextMeshPro updaten")_

---

## 7. Level Keuzemenu

**Omschrijving:**  
Maak een menu waarin de speler een level kiest.

**Leerdoelen:**

- UI knoppen gebruiken
- Meerdere scenes beheren
- Scene transitions gebruiken

**Stappenplan + Hints:**

1. Voeg UI-knoppen toe in je menu _(Hint: "Unity UI button maken")_
2. Laat elke knop een andere scene laden _(Hint: "Unity SceneManager.LoadScene via knop")_
3. Voeg terugknoppen toe in elk level _(Hint: "Unity UI button terug naar menu")_
4. Test of alles werkt zoals bedoeld _(Hint: "Unity scene wisselen debuggen")_

---

## 8. Automatische Structuren

**Omschrijving:**  
Laat het spel automatisch blokken genereren in een patroon zoals een trap.

**Leerdoelen:**

- Loops gebruiken
- Vector3 posities berekenen
- Patronen genereren

**Stappenplan + Hints:**

1. Teken je patroon uit (bv. trap) _(Hint: "Unity block trap design")_
2. Bedenk hoe je dat herhaalt in een loop _(Hint: "C# for loop Unity objecten")_
3. Bereken de locatie voor elk blok _(Hint: "Unity Vector3 berekening")_
4. Laat de blokken op hun plek verschijnen _(Hint: "Unity Instantiate object met positie")_
5. Voeg extra logica toe voor variatie _(Hint: "Unity patroon logica")_

---

## 9. Health + Damage voor vijanden

**Omschrijving:**  
Geef vijanden health en laat ze verdwijnen als dat op is.

**Leerdoelen:**

- Levenspunten bijhouden
- Objecten vernietigen bij 0 HP
- Feedback tonen bij schade

**Stappenplan + Hints:**

1. Bepaal hoeveel health de vijand heeft _(Hint: "Unity enemy health variabele")_
2. Zorg dat schade wordt toegepast _(Hint: "Unity detect hit damage")_
3. Trek health af bij elke hit _(Hint: "Unity -= health systeem")_
4. Verwijder de vijand als health 0 is _(Hint: "Unity Destroy bij 0 health")_
5. Geef visuele feedback bij schade _(Hint: "Unity flash or animation bij damage")_

---

## 10. Puzzel: juiste volgorde

**Omschrijving:**  
Laat een deur pas openen als knoppen in de juiste volgorde zijn geactiveerd.

**Leerdoelen:**

- Arrays en lijsten gebruiken
- Invoer vergelijken
- Interactie met triggers

**Stappenplan + Hints:**

1. Zet meerdere knoppen neer in de scène _(Hint: "Unity button trigger zones")_
2. Leg vast in welke volgorde ze ingedrukt moeten worden _(Hint: "Unity array juiste volgorde")_
3. Hou bij welke knoppen zijn ingedrukt _(Hint: "Unity lijst vullen bij input")_
4. Vergelijk met de juiste volgorde _(Hint: "Unity list vs array gelijkheid")_
5. Laat de deur alleen open gaan als het klopt _(Hint: "Unity actie bij correcte input")_

---

## 11. Checkpoint-systeem

**Omschrijving:**  
Laat de speler terugkeren naar het laatst bereikte checkpoint na een fout, zoals vallen of sterven.

**Leerdoelen:**

- Locaties opslaan
- Terugplaatsen van objecten
- Triggerdetectie

**Stappenplan + Hints:**

1. Plaats checkpoints in je scène _(Hint: "Unity checkpoint object maken")_
2. Detecteer wanneer een checkpoint geraakt wordt _(Hint: "Unity OnTriggerEnter checkpoint")_
3. Sla de positie van het checkpoint op _(Hint: "Unity Vector3 positie onthouden")_
4. Verplaats de speler terug na een fout _(Hint: "Unity reset player position")_
5. Test of de speler steeds bij het juiste checkpoint herstart _(Hint: "Unity debug respawn logic")_

---

## 12. Magneet-mechanic

**Omschrijving:**  
Laat objecten naar de speler toe getrokken worden als deze in de buurt komt.

**Leerdoelen:**

- Vectorberekening gebruiken
- Beweging automatisch aansturen
- Afstanden meten

**Stappenplan + Hints:**

1. Kies een object dat moet bewegen richting speler _(Hint: "Unity move object towards player")_
2. Meet voortdurend de afstand tot de speler _(Hint: "Unity Vector3.Distance")_
3. Bepaal de richting naar de speler _(Hint: "Unity vector richting berekenen")_
4. Beweeg het object geleidelijk richting de speler _(Hint: "Unity MoveTowards of Lerp")_
5. Laat iets gebeuren bij contact _(Hint: "Unity collision met speler")_

---

## 13. Highscore-systeem

**Omschrijving:**  
Laat een score vergelijken met een opgeslagen highscore. Bewaar de hoogste score lokaal.

**Leerdoelen:**

- Scores bijhouden en vergelijken
- Gegevens opslaan met PlayerPrefs
- UI updaten

**Stappenplan + Hints:**

1. Houd tijdens het spel een score bij _(Hint: "Unity score variabele bijhouden")_
2. Vergelijk die met de huidige highscore _(Hint: "Unity if score > highscore")_
3. Werk de highscore bij indien nodig _(Hint: "Unity PlayerPrefs.SetInt uitleg")_
4. Sla de score lokaal op _(Hint: "Unity highscore opslaan")_
5. Laat zowel score als highscore zien in UI _(Hint: "Unity TextMeshPro meerdere variabelen tonen")_

---

## 14. Bewegend platform

**Omschrijving:**  
Laat een platform bewegen tussen punten en de speler meebewegen als hij erop staat.

**Leerdoelen:**

- Lerp of MoveTowards toepassen
- Player parenting
- Beweging synchroniseren

**Stappenplan + Hints:**

1. Bepaal start- en eindpunten van het platform _(Hint: "Unity platform movement Vector3")_
2. Beweeg het platform tussen die punten _(Hint: "Unity Lerp voor platform")_
3. Zorg dat de speler erop blijft staan _(Hint: "Unity set parent op platform")_
4. Ontkoppel de speler bij verlaten _(Hint: "Unity player unparent on exit")_
5. Test gedrag bij rennen/springen op platform _(Hint: "Unity character op bewegend object")_

---

## 15. Dialogensysteem met keuzes

**Omschrijving:**  
Laat een NPC praten met de speler en geef de speler meerdere reacties om uit te kiezen.

**Leerdoelen:**

- UI-dialogen maken
- Condities en keuzes verwerken
- State management

**Stappenplan + Hints:**

1. Schrijf een dialoog met keuzes _(Hint: "Unity dialogue tree design")_
2. Laat tekstregels achter elkaar zien _(Hint: "Unity TextMeshPro typewriter effect")_
3. Voeg knoppen toe voor keuzes _(Hint: "Unity UI button interactie")_
4. Registreer de gemaakte keuze _(Hint: "Unity keuzedata opslaan")_
5. Laat de uitkomst variëren per keuze _(Hint: "Unity switch case voor dialoogkeuzes")_

---

## 16. Respawnende vijanden

**Omschrijving:**  
Laat vijanden na vernietiging na een paar seconden opnieuw verschijnen.

**Leerdoelen:**

- Destroy & Instantiate gebruiken
- Coroutines met timers
- Prefabs beheren

**Stappenplan + Hints:**

1. Vernietig vijand na 0 health _(Hint: "Unity enemy destroy bij 0 health")_
2. Start een timer zodra de vijand verdwijnt _(Hint: "Unity Coroutine met WaitForSeconds")_
3. Wacht een ingestelde tijd _(Hint: "Unity delay in Coroutine")_
4. Instantieer een nieuwe vijand op dezelfde plek _(Hint: "Unity Instantiate prefab at position")_
5. Zorg dat dit herhaalbaar is _(Hint: "Unity respawn loop implementeren")_

---

## 17. Richtkruis + schieten

**Omschrijving:**  
Laat de speler met een richtkruis en muisklikken objecten raken.

**Leerdoelen:**

- Raycasting gebruiken
- UI en camera combineren
- Interactie op afstand

**Stappenplan + Hints:**

1. Voeg een richtkruis toe in de UI _(Hint: "Unity crosshair overlay maken")_
2. Detecteer muisklikken _(Hint: "Unity Input.GetMouseButtonDown")_
3. Stuur een ray vanaf de camera _(Hint: "Unity raycast vanaf camera")_
4. Check of je iets raakt _(Hint: "Unity RaycastHit uitleg")_
5. Laat iets gebeuren bij raak _(Hint: "Unity trigger actie bij raycast hit")_

---

## 18. Glibberige vloer

**Omschrijving:**  
Maak een gebied waar de speler glijdt zoals op ijs.

**Leerdoelen:**

- Physics materials toepassen
- Input aanpassen per oppervlak
- Frictie instellen

**Stappenplan + Hints:**

1. Kies welk oppervlak glad moet zijn _(Hint: "Unity physics material maken")_
2. Pas een physics material toe met weinig wrijving _(Hint: "Unity friction settings aanpassen")_
3. Detecteer wanneer de speler op dat oppervlak is _(Hint: "Unity trigger of tag check")_
4. Pas de besturing aan tijdens contact _(Hint: "Unity movement modifier per ondergrond")_
5. Zet alles terug bij het verlaten van het oppervlak _(Hint: "Unity OnTriggerExit beweging reset")_

---

## 19. Verzamelvolgorde puzzel

**Omschrijving:**  
Laat objecten in een specifieke volgorde verzamelen om iets te activeren.

**Leerdoelen:**

- Lijst vergelijken met oplossing
- Condities controleren
- Interactieve logica opbouwen

**Stappenplan + Hints:**

1. Plaats meerdere verzamelobjecten _(Hint: "Unity collectable items toevoegen")_
2. Leg de correcte volgorde vast _(Hint: "Unity array volgorde vastleggen")_
3. Sla de opgepakte volgorde op _(Hint: "Unity lijst vullen bij oppakken")_
4. Vergelijk de lijsten _(Hint: "Unity list equals array")_
5. Activeer een gebeurtenis als de volgorde juist is _(Hint: "Unity event bij correcte input")_

---

## 20. Skin/uiterlijk wisselaar

**Omschrijving:**  
Laat de speler het uiterlijk van zijn karakter aanpassen via een menu.

**Leerdoelen:**

- Materialen of modellen wisselen
- UI interactie
- Gegevens onthouden

**Stappenplan + Hints:**

1. Maak meerdere visuele opties _(Hint: "Unity character customization maken")_
2. Bouw een UI-keuzemenu _(Hint: "Unity dropdown of button keuzes")_
3. Pas het uiterlijk aan na selectie _(Hint: "Unity materiaal wisselen in script")_
4. Laat het resultaat live zien _(Hint: "Unity karakter realtime bijwerken")_
5. Sla de keuze op met PlayerPrefs _(Hint: "Unity uiterlijk opslaan met PlayerPrefs")_

---
