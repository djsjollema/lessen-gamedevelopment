# Les 1: Rigidbody2D en Zwaartekracht

## Concept Uitleg

In Unity is `Rigidbody2D` een component die de fysica van 2D-objecten regelt. Dit omvat beweging, zwaartekracht en botsingen. Wanneer je een `Rigidbody2D` aan een GameObject toevoegt, begint het onderhevig te zijn aan krachten zoals zwaartekracht.

### Zwaartekracht

Zwaartekracht in 2D werkt normaal gesproken naar beneden (negatief Y-richting). Je kan dit configureren in de Inspector via:

- **Gravity Scale:** Hoe sterk de zwaartekracht is (standaard 1)
- **Constraints:** Welke assen vast zijn

### Praktisch Voorbeeld (Flappy Bird Context)

In Flappy Bird valt de vogel automatisch naar beneden door zwaartekracht, zonder dat je daar iets voor hoeft in te programmeren. Je stelt alleen in dat `Gravity Scale = 1`.

```csharp
public class Bird : MonoBehaviour
{
    private Rigidbody2D rb;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
        // Zwaartekracht werkt nu automatisch!
    }
}
```

## Oefening: Vallende Balletjes Simulator

### Doel

Maak een eenvoudige scene met vallende balletjes die door zwaartekracht naar beneden vallen.

### Stappen

1. **Setup**

   - Maak een leeg Project aan of open een bestaand
   - Creëer een 2D Scene

2. **Bouw de Scene**

   - Maak 3 Spheres (of andere shapes) aan
   - Voeg aan elk een `Rigidbody2D` component toe
   - Zet elk balletje op verschillende hoogte in de scene
   - Verander de Gravity Scale van elk balletje:
     - Balletje 1: Gravity Scale = 0.5 (langzaam vallend)
     - Balletje 2: Gravity Scale = 1.0 (normaal vallend)
     - Balletje 3: Gravity Scale = 2.0 (snel vallend)

3. **Vergelijk het Gedrag**
   - Speel de scene af
   - Observeer hoe de balletjes verschillende snelheden hebben
   - Noteer welk balletje het snelst valt

### Uitdaging

- Zet de Gravity Scale van twee balletjes op negatief (-1). Wat gebeurt er?
- Kan je een balletje recht houden zodat het niet zakt?

---

**Leerdoel:** Begrijpen hoe zwaartekracht werkt in Unity en hoe je het kan aanpassen.
