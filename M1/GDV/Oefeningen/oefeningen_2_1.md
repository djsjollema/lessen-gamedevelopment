# Oefeningen Les 2.1: Scenes, GameObjects en Scriptmatige Beweging

Kies 1 van de volgende oefeningen en voer die uit. Je mag er ook meer maken als je dat leuk vind en daar ook tijd voor over hebt.

## Inleveren werk

De oefeningen moeten jullie inleveren via een zogenaamde README.md file op Github.

Voor alle oefeningen geldt dat je een titel met de opdracht plaatst. Een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[gebruik dit als template](../README.md#voorbeeld-readme-opdracht-format)

## Oefening 2.1A: Animated Gaming Icons

### Doel

Leer GameObjects besturen met scripts door gaming iconen te animeren.

### Wat ga je doen?

Maak bewegende gaming iconen zoals een draaiende coin, huppelende power-up en zwevende health pack.

### Stappen

1. **Maak een nieuwe scene** genaamd "GamingIcons"
2. **Voeg deze GameObjects toe:**

   - **Coin:** Cylinder (geel materiaal)
   - **Power-up:** Sphere (groen materiaal)
   - **Health Pack:** Cube (rood materiaal)
   - **XP Orb:** Sphere (blauw materiaal)

3. **Maak bewegingsscripts:**

   **CoinRotator.cs:**

   ```csharp
   public class CoinRotator : MonoBehaviour
   {
       public float rotateSpeed = 90.0f; // graden per seconde

       void Update()
       {
           // Draai rond Y-as (zoals een echte coin)
           transform.Rotate(0, rotateSpeed * Time.deltaTime, 0);
       }
   }
   ```

   **PowerUpBounce.cs:**

   ```csharp
   public class PowerUpBounce : MonoBehaviour
   {
       public float bounceHeight = 1.0f;
       public float bounceSpeed = 2.0f;
       private Vector3 startPosition;

       void Start()
       {
           startPosition = transform.position;
       }

       void Update()
       {
           // Op en neer beweging
           float newY = startPosition.y + bounceHeight * Mathf.Sin(Time.time * bounceSpeed);
           transform.position = new Vector3(startPosition.x, newY, startPosition.z);
       }
   }
   ```

   **HealthPackFloat.cs:**

   ```csharp
   public class HealthPackFloat : MonoBehaviour
   {
       public float floatSpeed = 1.0f;
       public float rotateSpeed = 45.0f;

       void Update()
       {
           // Zweven en draaien
           transform.Translate(Vector3.up * floatSpeed * Time.deltaTime);
           transform.Rotate(rotateSpeed * Time.deltaTime, 0, 0);
       }
   }
   ```

4. **Voeg scripts toe aan de juiste objecten**
5. **Test in Play Mode** en pas snelheden aan naar wens

### Bonus Uitdagingen

- Voeg een **XPOrbOrbit.cs** script toe dat rond de speler draait
- Maak een **CollectibleGlow.cs** script dat de schaal laat pulseren
- Voeg geluideffecten toe (later in de cursus)
- Maak een spawn area waar nieuwe items verschijnen

---

## Oefening 2.1B: Solar System Simulator

### Doel

Bouw een mini zonnestelsel met planeten die rond de zon draaien.

### Wat ga je doen?

Maak een zonnestelsel waar planeten in banen rond de zon bewegen.

### Stappen

1. **Maak een nieuwe scene** genaamd "SolarSystem"
2. **Voeg GameObjects toe:**

   - **Zon:** Grote gele Sphere in het midden
   - **Aarde:** Blauwe Sphere
   - **Mars:** Rode Sphere (kleiner)
   - **Jupiter:** Grote oranje Sphere
   - **Saturnus:** Gele Sphere met Cylinder als ring

3. **Maak bewegingsscripts:**

   **SunRotator.cs:**

   ```csharp
   public class SunRotator : MonoBehaviour
   {
       public float rotationSpeed = 30.0f;

       void Update()
       {
           // Zon draait om eigen as
           transform.Rotate(0, rotationSpeed * Time.deltaTime, 0);
       }
   }
   ```

   **PlanetOrbit.cs:**

   ```csharp
   public class PlanetOrbit : MonoBehaviour
   {
       public Transform centerPoint; // Sleep de Zon hier naartoe
       public float orbitSpeed = 20.0f;
       public float orbitRadius = 5.0f;
       public float rotationSpeed = 100.0f;

       void Update()
       {
           if (centerPoint != null)
           {
               // Draai rond de zon
               transform.RotateAround(centerPoint.position, Vector3.up, orbitSpeed * Time.deltaTime);

               // Draai om eigen as
               transform.Rotate(0, rotationSpeed * Time.deltaTime, 0);
           }
       }
   }
   ```

4. **Setup de planeten:**
   - Plaats elke planeet op verschillende afstanden van de zon
   - Voeg PlanetOrbit script toe aan elke planeet
   - Sleep de Zon naar het "Center Point" veld
   - Geef elke planeet verschillende orbit en rotatie snelheden

### Bonus Uitdagingen

- Voeg **manen** toe die rond planeten draaien
- Maak een **AsteroidBelt.cs** script met veel kleine objecten
- Voeg **Comet.cs** toe met een elliptische baan
- Maak verschillende orbit snelheden realistischer (verder = langzamer)

---

## Oefening 2.1C: Retro Screen Saver Collection

### Doel

Maak klassieke screensavers zoals bouncing balls en floating logos.

### Wat ga je doen?

Bouw verschillende retro screensaver effecten die je kent van oude computers.

### Stappen

1. **Maak een nieuwe scene** genaamd "ScreenSavers"
2. **Voeg deze screensavers toe:**

   **BouncingBall.cs:**

   ```csharp
   public class BouncingBall : MonoBehaviour
   {
       public Vector3 velocity = new Vector3(3, 2, 0);
       public Vector3 screenBounds = new Vector3(8, 4, 0);

       void Update()
       {
           // Beweeg de bal
           transform.position += velocity * Time.deltaTime;

           // Check grenzen en stuiteren
           Vector3 pos = transform.position;

           if (pos.x > screenBounds.x || pos.x < -screenBounds.x)
           {
               velocity.x = -velocity.x; // Omkeren X richting
           }

           if (pos.y > screenBounds.y || pos.y < -screenBounds.y)
           {
               velocity.y = -velocity.y; // Omkeren Y richting
           }
       }
   }
   ```

   **FloatingLogo.cs:**

   ```csharp
   public class FloatingLogo : MonoBehaviour
   {
       public float moveSpeed = 2.0f;
       public float rotateSpeed = 30.0f;
       public Vector3 direction = Vector3.right;
       public Vector3 screenBounds = new Vector3(10, 6, 0);

       void Update()
       {
           // Beweeg in richting
           transform.position += direction * moveSpeed * Time.deltaTime;

           // Langzame rotatie
           transform.Rotate(0, 0, rotateSpeed * Time.deltaTime);

           // Wrap around screen (teleporteer naar andere kant)
           Vector3 pos = transform.position;

           if (pos.x > screenBounds.x)
               pos.x = -screenBounds.x;
           if (pos.x < -screenBounds.x)
               pos.x = screenBounds.x;
           if (pos.y > screenBounds.y)
               pos.y = -screenBounds.y;
           if (pos.y < -screenBounds.y)
               pos.y = screenBounds.y;

           transform.position = pos;
       }
   }
   ```

   **StarField.cs:**

   ```csharp
   public class StarField : MonoBehaviour
   {
       public float speed = 5.0f;
       public float resetDistance = 10.0f;

       void Update()
       {
           // Beweeg naar de camera toe
           transform.Translate(Vector3.forward * speed * Time.deltaTime);

           // Reset positie als te dichtbij
           if (transform.position.z > resetDistance)
           {
               Vector3 newPos = transform.position;
               newPos.z = -resetDistance;
               newPos.x = Random.Range(-8f, 8f);
               newPos.y = Random.Range(-4f, 4f);
               transform.position = newPos;
           }
       }
   }
   ```

3. **Setup de scene:**
   - **Bouncing Ball:** Maak een Sphere met BouncingBall script
   - **Floating Logo:** Maak een Cube met FloatingLogo script
   - **Star Field:** Maak 20 kleine witte Spheres met StarField script
   - Zet de camera zo dat je alles goed ziet

### Bonus Uitdagingen

- Voeg **kleur verandering** toe aan de bouncing ball bij elke stuit
- Maak een **Matrix Rain** effect met vallende tekst
- Voeg **trails** toe aan bewegende objecten
- Maak een **Pong** screensaver met twee paddles

---

## Tips voor Alle Oefeningen

### Movement Debugging

- Gebruik **Debug.Log()** om posities en snelheden te checken
- Voeg **Debug.DrawLine()** toe om bewegingspaden te visualiseren
- Test verschillende snelheidswaarden om het juiste gevoel te vinden

### Performance Tips

- Gebruik **public** variabelen voor snelheden die je wilt aanpassen
- Cache **Transform** referenties in Start() voor betere performance
- Vermijd **GetComponent()** calls in Update()

### Organization Tips

- Geef scripts **beschrijvende namen** (niet gewoon "Movement")
- Groepeer gerelateerde GameObjects in **empty parent objects**
- Gebruik **meaningful variable names** (rotateSpeed, niet speed1)

---
