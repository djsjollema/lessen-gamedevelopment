# Les 2.1 Week 2 – Forces & collision




## Waarom gebruiken we AddForce?

AddForce geeft een duw aan een Rigidbody.  
De Rigidbody is het onderdeel dat door Unity’s physics wordt bestuurd, dus daar moet de kracht naartoe.  
Wanneer je AddForce gebruikt, reageert de bal op zwaartekracht, massa en bouncen. Dat maakt de beweging natuurlijk.

Een Transform verplaatsen kan wel, maar dat is geen echte beweging. Je teleporteert de bal dan steeds een klein stukje. 
Dat ziet er onrealistisch uit en geeft geen botsingen, geen stuiteren en geen physics.

AddForce werkt samen met het physics-systeem. Daarom is het de juiste manier voor een Peggle-achtig spel waar één kracht wordt gegeven en daarna de natuurkunde het overneemt.


---

## Stap 1. 

- Maak een nieuw 2D project aan. 
![Universal 2D project](image.png)

Geef je project een naam waar jij en je docent meteen uit kunnen afleiden wat het is en van wie het is, bijvoorbeeld FruityPeggle_KimVerweij.

## Stap 1 - Level


## Stap 2 – Bal afschieten met AddForce

### 0. Maak een bal.
![alt text](image-1.png)

Geef het een GameObject een correcte naam zoals Bal.

--- 

### 1. Controleer of je bal een Rigidbody2D heeft
- Selecteer je bal in de scene.  
- Ga naar **Add Component** en kies **Rigidbody2D**.  

<img width="443" height="205" alt="image" src="https://github.com/user-attachments/assets/179d7f40-a0e6-4dbe-b11f-96de1fafe2e1" />


---

### 2. Zorg dat de bal een Collider heeft
- Gebruik een **CircleCollider2D** of een andere 2D-collider.  
Zonder collider zijn er geen botsingen.

<img width="442" height="214" alt="image" src="https://github.com/user-attachments/assets/a3da060f-e222-4bf6-807a-eabfcfd0e082" />



---

### 3. Voeg een 2D physics material toe
- Maak een folder aan genaamd Material.
- Open deze folder, right-click in deze folder en maak een Physics Material 2D aan.
<img width="766" height="328" alt="image" src="https://github.com/user-attachments/assets/60104bbb-45a2-4584-84eb-47fd37810c2f" />

Zonder physics material 2D heeft de bal geen bounce. 
- Voeg de material toe aan de collider (NIET AAN de RIGIDBODY)

---

### 4. Maak een script om de bal te schieten
- Maak een nieuw script, bijvoorbeeld **ShootBall.cs**.
- Voeg het script toe aan de bal.

Je kunt de opdracht helemaal zelf maken door de stappen hieronder te volgen. Lukt het niet of wil je je werk controleren?  
Dan kun je verderop de voorbeeldcode openen.

### Stappen om je op weg te helpen
1. Zorg dat je bal een Rigidbody2D heeft.
2. Maak een script dat luistert naar een toets (bijvoorbeeld A of Spatie).
3. Haal in Start() de Rigidbody2D op met GetComponent.
4. In Update(): wanneer je op de toets drukt, geef je een AddForce.
5. Test verschillende waardes voor richting en kracht.



<details>
<summary>Klik om de voorbeeldcode te openen</summary>
    
```csharp


// Hoe hard de bal wordt weggeduwd
public float ShootForce = 500f;

// In welke richting de bal duwt krijgt (0,1,0 = omhoog)
public Vector3 Direction = new Vector3(0f,1f,0f);

private Rigidbody2D rb;

// Start is called once before the first execution of Update after the MonoBehaviour is created
void Start()
{
    // aalt automatisch de Rigidbody2D op van dit object
    rb = GetComponent<Rigidbody2D>();
}

// Update is called once per frame
void Update()
{
    if(Input.GetKeyDown(KeyCode.A))
    {
        // Geeft een kracht in de opgegeven richting * sterkte
        rb.AddForce(Direction * ShootForce);
        
    }
}
```
</details>
