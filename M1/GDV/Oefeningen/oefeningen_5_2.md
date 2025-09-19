# Oefeningen Les 5.2: Logica Combineren met Botsingen en Input

Kies 1 van de volgende oefeningen en voer die uit. Je mag er ook meer maken als je dat leuk vindt en daar ook tijd voor over hebt.

## Inleveren werk

De oefeningen moeten jullie inleveren via een README.md file op Github.

Voor alle oefeningen geldt dat je een titel met de opdracht plaatst, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[gebruik dit als template](../README.md#voorbeeld-readme-opdracht-format)

---

## Oefening 5.2A: Slimme Pickup Systeem

### Doel

Combineer input, if-statements en collision detection door een pickup systeem te maken dat alleen werkt onder bepaalde voorwaarden.

### Wat ga je doen?

Je maakt een script waarin een speler alleen een health potion kan oppakken als zijn health niet vol is.

### Stappen

1. **Maak een nieuwe scene** genaamd "SmartPickup"
2. **Maak een Capsule als speler** met een variabele `int health` en `int maxHealth`
3. **Maak een Sphere als health potion** met een Collider (Is Trigger aan)
4. **Maak een script** `SmartPickup.cs` dat in `OnTriggerEnter` checkt:
   - Alleen oppakken als `health < maxHealth`
   - Verhoog health en vernietig het potion object
   - Toon een bericht in de console
5. **Test het systeem** door health te veranderen en te proberen op te pakken

#### Voorbeeld Console Output

```
Health restored!
Health already full!
```

### Bonus Uitdagingen

- Voeg een key pickup toe die alleen werkt als je nog geen key hebt
- Toon een visueel effect bij het oppakken
- Voeg een score systeem toe voor elke pickup

---

## Oefening 5.2B: Interactieve Deur met Sleutel

### Doel

Combineer input, if-statements en collision detection door een deur te maken die alleen opent als je een sleutel hebt.

### Wat ga je doen?

Je maakt een script waarin een speler een deur kan openen met de E-toets, maar alleen als hij een sleutel heeft.

### Stappen

1. **Maak een nieuwe scene** genaamd "DoorWithKey"
2. **Maak een Capsule als speler** met een bool `hasKey`
3. **Maak een Cube als deur** met een Collider (Is Trigger aan)
4. **Maak een script** `DoorWithKey.cs` dat in `OnTriggerEnter` een hint toont ("Press E to open")
5. **Laat de deur alleen openen** als de speler op E drukt en `hasKey == true`
6. **Test het systeem** door een sleutel op te pakken en de deur te openen

#### Voorbeeld Console Output

```
Press E to open (needs key)
Need a key!
Door opened!
```

### Bonus Uitdagingen

- Laat de deur omhoog bewegen als hij opent
- Toon een ander bericht als je geen sleutel hebt
- Voeg een animatie toe aan de deur

---

## Oefening 5.2C: Game State Manager (Zonder Enum)

### Doel

Combineer input, if-statements en variabelen door een simpel game state systeem te maken.

### Wat ga je doen?

Je maakt een script waarin je tussen verschillende game states kunt wisselen (Playing, Paused, GameOver) en de juiste acties uitvoert, zonder gebruik van een enum.

### Stappen

1. **Maak een nieuwe scene** genaamd "GameStateManager"
2. **Maak een script** `GameStateManager.cs` met een variabele `string gameState` (of `int gameState`)
   - Bijvoorbeeld: `"Playing"`, `"Paused"`, `"GameOver"`
3. **Gebruik toetsen** om van state te wisselen:
   - Escape = pauzeren/hervatten
   - R = opnieuw starten bij GameOver
4. **Gebruik if-statements** om te bepalen wat er gebeurt in elke state
5. **Toon een bericht in de console** bij elke state wissel
6. **Test het systeem** door te wisselen tussen states

#### Voorbeeld Console Output

```
Game Paused - Press ESC to resume
Game Resumed
GAME OVER! Press R to restart
Game Restarted
```

### Bonus Uitdagingen

- Voeg een score en lives systeem toe
- Laat het spel automatisch GameOver gaan als lives 0 zijn
- Toon een visueel effect bij elke state wissel

---
