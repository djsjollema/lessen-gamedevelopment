**Niveau beginner:**

- **PlayerMove.cs**:

```csharp
using UnityEngine;

public class PlayerMove : MonoBehaviour
{
    [SerializeField] private float speed = 20f; //Snelheid van de speler
    void Update()
    {
        //bereken de beweging over de x en z as nav de horizontale en verticale input
        float moxeX = Input.GetAxis("Horizontal") * speed * Time.deltaTime;
        float moxeZ = Input.GetAxis("Vertical") * speed * Time.deltaTime;
        Vector3 move = new Vector3(moxeX, 0f, moxeZ);
        //beweeg het gameobject
        transform.Translate(move);
    }
}
```

- **FollowAndReturn.cs**:

```csharp
using UnityEngine;
public class FollowAndReturn : MonoBehaviour
{
    public float returnSpeed = 5f;       // Snelheid waarmee de follower terug gaat naar het startpunt
    public Transform target;            // Doel om the achtervolgen (sleep in Inspector)
    private Vector3 startPosition;      // Startpositie van het volger object
    private bool isResetting = ...;   // Schakelaar voor resetten / terugkeren naar het startpunt.

    void Start()
    {
        // Sla de startpositie van dit object op
        startPosition = ...;
    }
    void Update()
    {
        //Roep ReturnToStart() aan als isRestting true is en anders roep je FollowTarget() aan
        if (isResetting) ...
        else ...;
    }
    private void FollowTarget()
    {
        // Gebruik de Lerp(a,b,c) methode om van de huidige positie (a) naar het doel (b) te bewegen. Doe dit met een percentage (c) van de afstand 0.1f is 10%
        transform.position = Vector3.Lerp(..., ..., ...);

        // Bereken de afstand tussen de volger en de target (de speler). Doe dit met Vector3.Distance(a,b)
        float distance = Vector3.Distance(... , ...);
        // Geef de distance weer in de console
        Debug.Log("distance to player: " + ...);
        // check of de target is bereikt door te checken of de distance klein genoeg is( < 0.1f)
        // Zet de boolean isResetting op true
        if (... < 0.1f) ...;
    }
    private void ReturnToStart()
    {
        // Verplaats de volger naar startpositie met een vaste snelheid.

        //bereken de genormaliseerde (enkele stap) richting van de volger naar zijn startpunt
        Vector3 direction = (startPosition - transform.position).... ;
        //Beweeg de volger in deze richting met een vaste snelheid. Gebruik hiervoor de returnSpeed variabele.
        transform.Translate(... * ... * Time.deltaTime);

        // Bereken de afstand tussen de startpositie en de positie van de volger
        float distToStart = Vector3.Distance(... , ...);
        // Zet de boolean isResetting weer op false als de speler bijna (< 0.1f) op de startpositie teruggekeerd is
        if (... < 0.1f) ...;
    }
}
```
