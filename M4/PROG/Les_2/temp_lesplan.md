### Lesplan: Instructieles Unity-specifieke Basisvaardigheden (30 minuten)

#### Doel

Studenten leren Unity-specifieke basisvaardigheden: `MonoBehaviour` begrijpen, `GameObjects` manipuleren, componenten gebruiken, en input verwerken. Na de les kunnen ze deze vaardigheden toepassen in een Unity-opdracht om een bewegende speler te maken.

#### Benodigdheden

- Laptop met Unity en Visual Studio geïnstalleerd.
- Projector/beamer voor demo’s.
- Voorbeeldbestand in Unity (scène met een speler-cube en een vloer).

#### Tijdsindeling

| **Tijd**      | **Activiteit**                    | **Details**                                                                                 |
| ------------- | --------------------------------- | ------------------------------------------------------------------------------------------- |
| **0-5 min**   | **Introductie en doel**           | Uitleg: "Vandaag leren we hoe Unity werkt met C#: scripts, objecten, componenten en input." |
| **5-10 min**  | **`MonoBehaviour` begrijpen**     | Demo: Toon `Start()` en `Update()` in een script, laat een bericht verschijnen bij start.   |
| **10-15 min** | **`GameObjects` manipuleren**     | Demo: Verplaats een cube met `transform.position` in `Update()`.                            |
| **15-20 min** | **Componenten gebruiken**         | Demo: Voeg een `Rigidbody` toe en gebruik `AddForce` voor een sprong.                       |
| **20-25 min** | **Input verwerken**               | Demo: Laat de cube bewegen met `Input.GetKey` (bijv. pijltjestoetsen).                      |
| **25-30 min** | **Samenvatting en opdrachtintro** | Recap: "Dit zijn Unity’s basis-tools!" Introduceer opdracht kort.                           |

#### Lesverloop

1. **Introductie (5 min)**

   - Vertel: "In les 1 leerden we C#. Nu gaan we die code gebruiken in Unity om dingen te laten gebeuren in een game."
   - Laat een simpel Unity-project zien (cube op een vloer).

2. **`MonoBehaviour` begrijpen (5 min)**

   - Leg uit: "`MonoBehaviour` is de basis van elk Unity-script. `Start()` gebeurt één keer, `Update()` elke frame."
   - Demo: Maak een script `PlayerControl` met `void Start() { Debug.Log("Speler klaar!"); }`. Start de scène en toon de console.

3. **`GameObjects` manipuleren (5 min)**

   - Leg uit: "Met `transform` kun je objecten verplaatsen, draaien of schalen."
   - Demo: Voeg toe: `void Update() { transform.position += Vector3.right * 0.01f; }`. Laat de cube bewegen.

4. **Componenten gebruiken (5 min)**

   - Leg uit: "Componenten zoals `Rigidbody` voegen physics toe. We kunnen ze aanroepen in code."
   - Demo: Voeg een `Rigidbody` toe aan de cube in Unity. In het script: `public Rigidbody rb; void Start() { rb = GetComponent<Rigidbody>(); }` en `if (Input.GetKeyDown(KeyCode.Space)) { rb.AddForce(Vector3.up * 5, ForceMode.Impulse); }`. Laat de cube springen.

5. **Input verwerken (5 min)**

   - Leg uit: "Met `Input` lees je wat de speler doet, zoals toetsen indrukken."
   - Demo: Voeg toe: `void Update() { if (Input.GetKey(KeyCode.RightArrow)) { transform.position += Vector3.right * 0.05f; } }`. Laat de cube naar rechts bewegen.

6. **Samenvatting en opdrachtintro (5 min)**
   - Recap: "We hebben geleerd hoe Unity-scripts werken, objecten bewegen, componenten gebruiken en input lezen."
   - Intro opdracht: "Jullie gaan een speler maken die beweegt en springt!"

---

### Opdracht 2: "Bewegende Speler" (1,5 uur)

#### Doel

Studenten maken een Unity-scène met een speler die beweegt en springt, met gebruik van de vaardigheden uit deel 2.

#### Opdrachtbeschrijving

Maak een Unity-scène met een speler (cube) die kan bewegen met pijltjestoetsen en springen met de spatiebalk. Gebruik een `Rigidbody` voor physics en zorg dat de speler op een vloer blijft.

#### Stappen

1. **Setup (15 min)**

   - Maak een nieuwe Unity-scène.
   - Voeg een cube toe als "speler" en een plane als "vloer".
   - Voeg een `Rigidbody`-component toe aan de cube en een nieuw script `PlayerControl.cs`.

2. **Script schrijven (60 min)**

Er zijn 2 niveaus voor de opdracht om te differentieren: (beginner en gevorderd)

**Niveau beginner:**

```csharp
using UnityEngine;

public class PlayerControl : MonoBehaviour
{
   public Rigidbody rb;           // Referentie naar Rigidbody
   public ... moveSpeed = 5f;   // Snelheid van bewegen
   public ... jumpForce = 5f;   // Kracht van sprong

   void Start()
   {
         // Haal Rigidbody op
         rb = GetComponent<Rigidbody>();
         Debug.Log("Speler klaar!");
   }

   void Update()
   {
         //Zorg dat het blokje naar links en rechts kan bewegen met de snelheid moveSpeed
         float input = Input.GetAxis(...);
         transform.... += Vector3.right * input * ... * Time.deltaTime;

         // Omhoog springen met spatie en een AddForce op de rigidbody
         if (Input.GetKeyDown(KeyCode....))
         {
            rb....(Vector3.... * jumpForce, ForceMode.Impulse);
         }
   }
}
```

**Niveau gevorderd:**

```csharp
using UnityEngine;

public class PlayerControl : MonoBehaviour
{
   // Referentie naar Rigidbody
   // Snelheid van bewegen moveSpeed type float
   // Kracht van sprong jumpForce type float

   void Start()
   {
         // Haal Rigidbody component op van het gameobject
         Debug.Log("Speler klaar!");
   }

   void Update()
   {
         // Beweging met pijltjestoetsen
         // Beweeg blokje naar links en rechts met de pijltjestoetsen

         // Simpele Sprong met spatie , gebruik rigidbody

   }
}
```

**Uitwerking:**

```csharp
using UnityEngine;

public class PlayerControl : MonoBehaviour
{
   public Rigidbody rb;           // Referentie naar Rigidbody
   public float moveSpeed = 5f;   // Snelheid van bewegen
   public float jumpForce = 5f;   // Kracht van sprong

   void Start()
   {
         // Haal Rigidbody op
         rb = GetComponent<Rigidbody>();
         Debug.Log("Speler klaar!");
   }

   void Update()
   {
         //Zorg dat het blokje naar links en rechts kan bewegen met de snelheid moveSpeed
         float input = Input.GetAxis("Horizontal");
         transform.position += Vector3.right * input * moveSpeed * Time.deltaTime;

         // Omhoog springen met spatie en een AddForce op de rigidbody
         if (Input.GetKeyDown(KeyCode.Space))
         {
            rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
         }
   }
}
```

- Test in Unity: gebruik pijltjestoetsen om te bewegen en spatie om te springen.

3. **Uitbreiding (15 min)**
   - Maak `moveSpeed` en `jumpForce` public en pas ze aan in de Inspector (probeer bijv. 7f en 10f).
   - Voeg een `Debug.Log("Springen!");` toe bij de sprong om te zien wanneer het werkt.

#### Beoordeling

- Beweegt de speler soepel met pijltjestoetsen?
- Werkt de sprong met de `Rigidbody`?
- Wordt `Start()` correct gebruikt (zie console)?
- Reageert de input goed?

#### Tijd

- **Instructie**: 30 minuten.
- **Opdracht**: 90 minuten (1,5 uur):
  - 15 min setup, 60 min basisscript, 15 min uitbreiding en testen.

---

### Toelichting

- **Les**: Kort, visueel en hands-on, met demo’s in Unity die aansluiten bij les 1 (C# basis). Elke vaardigheid wordt live getoond.
- **Opdracht**: Bouwt voort op les 1 (input en variabelen) en introduceert Unity-specifieke concepten (GameObjects, componenten). Het is een simpele maar complete mechanic, haalbaar in 1,5 uur.
- **Niveau**: Consistent met les 1, geschikt voor beginners met basiskennis van C#.

```

```
