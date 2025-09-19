# Oefeningen Les 4.1: Colliders, Triggers en Tags

Kies 1 van de volgende oefeningen en voer die uit. Je mag er ook meer maken als je dat leuk vindt en daar ook tijd voor over hebt.

## Inleveren werk

De oefeningen moeten jullie inleveren via een README.md file op Github.

Voor alle oefeningen geldt dat je een titel met de opdracht plaatst, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[gebruik dit als template](../README.md#voorbeeld-readme-opdracht-format)

---

## Oefening 4.1A: Pickup Zone Challenge

### Doel

Leer werken met Trigger Colliders en Tags door een pickup zone te maken.

### Wat ga je doen?

Je maakt een pickup item dat alleen reageert als de speler (met de juiste tag) het aanraakt.

### Stappen

1. **Maak een nieuwe scene** genaamd "PickupZone"
2. **Voeg een Capsule toe** als speler en geef deze de tag "Player"
3. **Voeg een Sphere toe** als pickup en geef deze de tag "Pickup"
4. **Zet "Is Trigger" aan** op de Sphere Collider van het pickup item
5. **Maak een script** `PickupZone.cs` dat een Debug.Log geeft als de speler het pickup item aanraakt
6. **Test het systeem** door de speler naar het pickup item te bewegen

#### Voorbeeld Console Output

```
Player entered the pickup zone!
Pickup collected!
```

### Bonus Uitdagingen

- Maak het pickup item transparant met een materiaal
- Voeg een tweede pickup toe met een andere tag ("PowerUp")
- Laat alleen spelers met de tag "Player" het item oppakken

---

## Oefening 4.1B: Checkpoint Tag System

### Doel

Oefen met Tags en Colliders door een checkpoint systeem te maken.

### Wat ga je doen?

Je maakt meerdere checkpoints die alleen reageren op objecten met de tag "Player".

### Stappen

1. **Maak een nieuwe scene** genaamd "Checkpoints"
2. **Voeg meerdere Cubes toe** als checkpoints en geef ze de tag "Checkpoint"
3. **Zet "Is Trigger" aan** op de Box Collider van elke checkpoint
4. **Maak een Capsule als speler** en geef deze de tag "Player"
5. **Maak een script** `CheckpointTrigger.cs` dat een Debug.Log geeft als de speler een checkpoint raakt
6. **Test het systeem** door de speler langs de checkpoints te bewegen

#### Voorbeeld Console Output

```
Player reached checkpoint 1!
Player reached checkpoint 2!
```

### Bonus Uitdagingen

- Geef elke checkpoint een uniek nummer of naam
- Laat checkpoints alleen één keer reageren per speler
- Toon een visueel effect bij het bereiken van een checkpoint

---

## Oefening 4.1C: Enemy Detection Zone

### Doel

Oefen met Trigger Colliders en Tags door een detectie zone voor vijanden te maken.

### Wat ga je doen?

Je maakt een zone die een melding geeft als een vijand (met de tag "Enemy") binnenkomt.

### Stappen

1. **Maak een nieuwe scene** genaamd "EnemyDetection"
2. **Voeg een Cube toe** als detectie zone en zet "Is Trigger" aan
3. **Geef de Cube de tag "DetectionZone"**
4. **Voeg een Sphere toe** als vijand en geef deze de tag "Enemy"
5. **Maak een script** `EnemyDetection.cs` dat een Debug.Log geeft als een vijand de zone binnenkomt
6. **Test het systeem** door de vijand naar de zone te bewegen

#### Voorbeeld Console Output

```
Enemy detected in zone!
```

### Bonus Uitdagingen

- Laat de zone een alarm afgaan (kleur veranderen)
- Voeg meerdere vijanden toe met verschillende tags
- Laat de zone ook reageren als de speler binnenkomt, maar met een andere melding

---
