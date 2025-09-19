# Oefeningen Les 5.1: If-Statements en Switch Gebruiken

Kies 1 van de volgende oefeningen en voer die uit. Je mag er ook meer maken als je dat leuk vindt en daar ook tijd voor over hebt.

## Inleveren werk

De oefeningen moeten jullie inleveren via een README.md file op Github.

Voor alle oefeningen geldt dat je een titel met de opdracht plaatst, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[gebruik dit als template](../README.md#voorbeeld-readme-opdracht-format)

---

## Oefening 5.1A: Health Status Indicator

### Doel

Oefen met if, else if en else door een health status systeem te maken.

### Wat ga je doen?

Je maakt een script dat de gezondheid van een speler controleert en verschillende berichten toont afhankelijk van de waarde.

### Stappen

1. **Maak een nieuwe scene** genaamd "HealthStatus"
2. **Maak een script** `HealthStatus.cs` met een variabele `int health`
3. **Gebruik if, else if en else** om verschillende statusberichten te tonen in de console:
   - health > 80: "Excellent health!"
   - health > 50: "Good health!"
   - health > 20: "Warning: Low health!"
   - anders: "Critical: Very low health!"
4. **Laat health afnemen** met een toets (bijvoorbeeld H) en verhogen met een andere toets (bijvoorbeeld J)
5. **Test het systeem** door health te veranderen en de juiste berichten te tonen

#### Voorbeeld Console Output

```
Excellent health!
Warning: Low health!
Critical: Very low health!
```

### Bonus Uitdagingen

- Voeg een visueel effect toe bij elke status (kleur veranderen)
- Toon een "Game Over" bericht als health 0 is
- Voeg een heal item toe dat health herstelt

---

## Oefening 5.1B: Weapon Switch System

### Doel

Oefen met switch-statements door een wapenwissel systeem te maken.

### Wat ga je doen?

Je maakt een script waarin je tussen verschillende wapens kunt wisselen en bij elk wapen andere stats toont.

### Stappen

1. **Maak een nieuwe scene** genaamd "WeaponSwitch"
2. **Maak een script** `WeaponSwitch.cs` met een variabele `string currentWeapon`
3. **Gebruik een switch-statement** om damage en attack speed te bepalen:
   - "Sword": damage 25, speed 1.0
   - "Bow": damage 20, speed 1.5
   - "Staff": damage 35, speed 0.7
   - "Dagger": damage 15, speed 2.0
   - default: damage 10, speed 1.0
4. **Wissel van wapen** met toetsen (1-4) en toon de stats in de console
5. **Test het systeem** door te wisselen en te zien dat de stats veranderen

#### Voorbeeld Console Output

```
Equipped: Sword
Damage: 25, Speed: 1
Equipped: Bow
Damage: 20, Speed: 1.5
```

### Bonus Uitdagingen

- Voeg een "Unarmed" optie toe als default
- Toon een korte beschrijving bij elk wapen
- Voeg een visueel model wissel toe bij wapen switch

---

## Oefening 5.1C: NPC Dialogue Choices

### Doel

Oefen met switch-statements en logische operatoren door een dialoog systeem te maken.

### Wat ga je doen?

Je maakt een script waarin een NPC verschillende antwoorden geeft afhankelijk van de keuze van de speler.

### Stappen

1. **Maak een nieuwe scene** genaamd "NPCDialogue"
2. **Maak een script** `NPCDialogue.cs` met een variabele `int dialogueStage`
3. **Gebruik een switch-statement** om verschillende dialogen te tonen:
   - 1: "Welkom, held!"
   - 2: "Kun je ons helpen?"
   - 3: "Er is een draak in het bos."
   - 4: "Wil je de quest accepteren?"
   - 5: "Bedankt! Je bent onze hoop."
   - default: "Succes op je avontuur!"
4. **Laat de speler verder gaan** met een toets (bijvoorbeeld E) en toon de juiste tekst
5. **Test het systeem** door door de dialogen te klikken

#### Voorbeeld Console Output

```
Welkom, held!
Kun je ons helpen?
Er is een draak in het bos.
Wil je de quest accepteren?
Bedankt! Je bent onze hoop.
Succes op je avontuur!
```

### Bonus Uitdagingen

- Voeg een keuze toe (Y/N) bij de quest acceptatie
- Toon een andere dialoog als de speler weigert
- Voeg een visueel effect toe bij elke dialoog stage

---
