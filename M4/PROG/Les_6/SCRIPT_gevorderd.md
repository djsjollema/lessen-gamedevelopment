**Niveau gevorderd:**

- **PlayerMove.cs**:

```csharp
using UnityEngine;

public class PlayerMove : MonoBehaviour
{
    //Zorg dat de speler over de x en z as bestuurd kan worden
}
```

- **FollowAndReturn.cs**:

```csharp
using UnityEngine;
public class FollowAndReturn : MonoBehaviour
{
    //volg de instructies in de comments en bepaal zelf welke variabelen je nodig hebt.
    void Start()
    {
        // Sla de startpositie op in een Vector3

    }
    void Update()
    {
        //Roep ReturnToStart() of FollowTarget() aan. Nooit allebei of geen van beiden.
        //Gebruik hiervoor een boolean isReturning

    }
    private void FollowTarget()
    {
        // Verander de positie van dit object met behulp van de Lerp methode
        // zorg dat de snelheid instelbaar is vanuit de inspector
        transform.position = Vector3.Lerp(...);

        // Bereken de afstand tussen dit object en een target. Gebruik de Distance methode of de .magnitude eigenschap
        // Geef deze target mee via de inspector.

        // check of de target is bereikt is de afstand klein genoeg? zet dan je boolean om zodat het object terug gaat naar de startpositie.
        if (...) //switch boolean;
    }
    private void ReturnToStart()
    {
        // Beweeg het object terug naar de startpositie met een vaste snelheid.
        //Bereken hiervoor de genormaliseerde (enkele stap) richting naar het startpunt.
        //Om de richting te bepalen trek je de huidige positie af van de doelpositie. (goalposition - currentposition)
        //Dit levert de totale afstand op. Die normaliseer je zodat je een enkele stap krijgt.

        Vector3 directionStep = ...;

        //Beweeg het object met de Translate methode. Gebruik een instelbare snelheid in de inspector en zorg dat het vloeiend beweegt op elke computer.

        transform.Translate(directionStep * ... * ...);

        // Bereken de afstand tussen dit object en de startpositie
        //Je mag zeft kiezen of je de Distance methode of de .magnitude eigenschap gebruikt.

        float distToStart = ...;
        // Stop het resetten als de speler bijna op de startpositie is dus als de afstand kleiner is dan bijvoorbeeld 0.1f
    }
}
```
