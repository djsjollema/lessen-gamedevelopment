# Oefeningen Les 3.1: Physics-componenten en Botsingen

Kies 1 van de volgende oefeningen en voer die uit. Je mag er ook meer maken als je dat leuk vindt en daar ook tijd voor over hebt.

## Inleveren werk

De oefeningen moeten jullie inleveren via een README.md file op Github.

Voor alle oefeningen geldt dat je een titel met de opdracht plaatst, een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[gebruik dit als template](../README.md#voorbeeld-readme-opdracht-format)

---

## Oefening 3.1A: Basketbal Dunk Simulator

### Doel

Oefen met Rigidbody, krachten en colliders door een basketbal te laten stuiteren en dunken.

### Wat ga je doen?

Je maakt een basketbal die kan stuiteren op de vloer en in een basket kan worden gegooid met physics.

### Stappen

1. **Maak een nieuwe scene** genaamd "BasketbalDunk"
2. **Voeg een Sphere toe** als basketbal, geef deze een oranje materiaal.
3. **Voeg een Plane toe** als vloer en een Cube als basket (boven de vloer).
4. **Voeg een Rigidbody toe** aan de basketbal.
5. **Voeg een Box Collider toe** aan de basket (Cube).
6. **Maak een script** `BasketballController.cs` waarmee je met de spatiebalk de bal omhoog laat springen (`AddForce`).
7. **Test het stuiteren en probeer te scoren!**

### Bonus Uitdagingen

- Maak de bal extra stuiterig met een Physics Material.
- Tel het aantal scores met een script.
- Voeg een scorebord toe met Debug.Log.

---

## Oefening 3.1B: Ruimte Asteroïde Botsing

### Doel

Oefen physics door een asteroïde te laten bewegen en botsen met een ruimteschip.

### Wat ga je doen?

Je maakt een asteroïde die door de ruimte zweeft en botst tegen een ruimteschip, beide reageren met physics.

### Stappen

1. **Maak een nieuwe scene** genaamd "AsteroidCollision"
2. **Voeg een Sphere toe** als asteroïde, geef deze een grijs materiaal.
3. **Voeg een Cube toe** als ruimteschip, plaats deze in het pad van de asteroïde.
4. **Voeg Rigidbody en Collider toe** aan beide objecten.
5. **Maak een script** `AsteroidMover.cs` dat de asteroïde een kracht geeft richting het schip (`AddForce` in `Start()`).
6. **Test de botsing en kijk hoe beide objecten reageren.**

### Bonus Uitdagingen

- Laat het schip wegschieten bij botsing.
- Voeg een Physics Material toe voor extra stuiter of wrijving.
- Log de snelheid van de asteroïde bij impact.

---

## Oefening 3.1C: Fantasy Springende Kist

### Doel

Oefen physics door een magische kist te laten springen en botsen op een fantasy vloer.

### Wat ga je doen?

Je maakt een kist die met een magische kracht kan springen en botst op een vloer, alles met physics.

### Stappen

1. **Maak een nieuwe scene** genaamd "MagicChest"
2. **Voeg een Cube toe** als kist, geef deze een fantasy kleur.
3. **Voeg een Plane toe** als vloer, geef deze een magisch materiaal.
4. **Voeg een Rigidbody toe** aan de kist.
5. **Maak een script** `MagicChestController.cs` waarmee je met de spatiebalk de kist laat springen (`AddForce`).
6. **Test het springen en botsen van de kist.**

### Bonus Uitdagingen

- Voeg een Particle System toe bij het springen.
- Maak de vloer extra glad of stuiterig met een Physics Material.
- Tel het aantal sprongen met Debug.Log.

---
