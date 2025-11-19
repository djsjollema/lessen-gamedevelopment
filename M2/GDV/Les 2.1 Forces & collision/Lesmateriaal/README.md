# Les 2.1 Week 2 – Forces & collision




## Waarom gebruiken we AddForce?

AddForce geeft een duw aan een Rigidbody.  
De Rigidbody is het onderdeel dat door Unity’s physics wordt bestuurd, dus daar moet de kracht naartoe.  
Wanneer je AddForce gebruikt, reageert de bal op zwaartekracht, massa en bouncen. Dat maakt de beweging natuurlijk.

Een Transform verplaatsen kan wel, maar dat is geen echte beweging. Je teleporteert de bal dan steeds een klein stukje. 
Dat ziet er onrealistisch uit en geeft geen botsingen, geen stuiteren en geen physics.

AddForce werkt samen met het physics-systeem. Daarom is het de juiste manier voor een Peggle-achtig spel waar één kracht wordt gegeven en daarna de natuurkunde het overneemt.


---

## S

Stap 1. 

Maak een nieuw 2D project aan. 
![Universal 2D project](image.png)

Geef het project een naam 

## Stap 1 - Level
Maak een 

## Stap 2 – Bal afschieten met AddForce

Maak een bal.
![alt text](image-1.png)


### 1. Controleer of je bal een Rigidbody2D heeft
Selecteer je bal in de scene.  
Ga naar **Add Component** en kies **Rigidbody2D**.  
Zorg dat *Gravity Scale* aan staat (standaard is 1).

### 2. Zorg dat de bal een Collider heeft
Gebruik een **CircleCollider2D** of een andere 2D-collider.  
Zonder collider zijn er geen botsingen.

### 3. Richt je kanon
Zorg dat jouw kanon in de richting wijst waarin je wilt schieten.  
In 2D gebruik je **transform.up** als schietrichting.

### 4. Maak een script om de bal te schieten
Maak een nieuw script, bijvoorbeeld **ShootBall.cs**.

```csharp
public Rigidbody2D rb;
public float force = 500f;

void Update()
{
    if (Input.GetKeyDown(KeyCode.Space))
    {
        rb.AddForce(transform.up * force);
    }
}