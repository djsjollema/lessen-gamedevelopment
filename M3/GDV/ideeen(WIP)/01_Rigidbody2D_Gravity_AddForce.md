# Les 1: Rigidbody2D, Zwaartekracht en AddForce

## Concept Uitleg

In Unity is `Rigidbody2D` een component die de fysica van 2D-objecten regelt. Dit omvat beweging, zwaartekracht en botsingen. Wanneer je een `Rigidbody2D` aan een GameObject toevoegt, begint het onderhevig te zijn aan krachten zoals zwaartekracht.

### Zwaartekracht

Zwaartekracht in 2D werkt normaal gesproken naar beneden (negatief Y-richting). Je kan dit configureren in de Inspector via:

- **Gravity Scale:** Hoe sterk de zwaartekracht is (standaard 1)
- **Constraints:** Welke assen vast zijn

### AddForce

In Flappy Bird valt de vogel automatisch naar beneden door zwaartekracht, zonder dat je daar iets voor hoeft in te programmeren. Je stelt alleen in dat `Gravity Scale = 1`.

Om de vogel toch naar boven te duwen kun je de Methode `AddForce()` gebruiken. Hiermee kun je een object met een `Rigidbody2D` component een kracht meegeven in een bepaalde richting.

```csharp
public class Bird : MonoBehaviour
{
   [SerializeField]private float force = 300f;
   private Rigidbody2D rb;

   void Start()
   {
         rb = GetComponent<Rigidbody2D>();
        // Zwaartekracht werkt nu automatisch!
   }
   void Update()
   {
         if(Input.GetKeyDown(KeyCode.return)){
            rb.AddForce(Vector2.up * force, ForceMode2D.Impulse);
            //Geef een kracht mee in een bepaalde richting
         }


   }
}
```

## Oefening: Hoog houden van een bal

### Doel

Maak een eenvoudige scene met daarin een 3 ballen met een `Rigidbody2d` component.
Voeg een script toe aan elke bal waarmee je hem hoog kunt houden door op de **1-toets**, de **2-toets** en de **3-toets** te drukken.

### Stappen

1. **Setup**
   - Maak een leeg Project aan of open een bestaand
   - Creëer een 2D Scene

2. **Bouw de Scene**
   - Maak 3 circles (of andere shapes) aan
   - Voeg aan elk een `Rigidbody2D` component toe
   - Zet elk balletje op verschillende hoogte in de scene
   - Verander de Gravity Scale van elk balletje:
     - Balletje 1: Gravity Scale = 0.5 (langzaam vallend)
     - Balletje 2: Gravity Scale = 1.0 (normaal vallend)
     - Balletje 3: Gravity Scale = 2.0 (snel vallend)

3. **Scrijf een script**
   - Zorg dat je 1 script schrijft die je voor alle ballen kunt hergebruiken. Noem deze `BallHop`.
   - Maak de `force` variabele instelbaar via de inspector met `[SerializeField]`
   - Laat alle ballen met een andere kracht de lucht in springen als je op de **spatie** drukt.

4. **Test en lever in**
   - Zorg dat je voor alle GDV opdrachten van deze periode een repository hebt op github
   - Zet de titel van de opdracht in je readme.
   - Omschrijf kort wat de opdracht was en wat je hebt gemaakt.
   - Demonstreer de uitwerking van de opdracht in een gifje.
   - Zet er een link naar de bijhorende code bij.

---

**Leerdoelen:** Begrijpen hoe zwaartekracht werkt in Unity en hoe je het kan aanpassen. Begrijpen hoe je `AddForce()` gebruikt om objecten in beweging te zetten.
