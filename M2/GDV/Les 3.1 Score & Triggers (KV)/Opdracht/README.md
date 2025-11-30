# Les 3.1 Week 3 – Score & Triggers Stappenplan


## Inleiding

In deze opdracht bouw je jouw eerste volledige Peggle-mechanic. Een Peggle is een object dat zelf kan bijhouden hoe vaak het geraakt is, punten oplevert en uiteindelijk verdwijnt wanneer de hits op zijn. Je gebruikt hiervoor je bestaande schietmechanic en ScoreManager.


---

## Stappenplan 
Maak een Peggle-object in je scene. Dit kan een sprite, een vorm of een eigen asset zijn. Geef het object een duidelijke naam, bijvoorbeeld Peggle of TargetFruit. Voeg een Collider2D toe zodat je bal de Peggle kan raken. Dit object heeft geen Rigidbody nodig.

Stap 2
Maak een nieuw script voor de Peggle. Voeg daarin twee instellingen toe: het totale aantal hits dat de Peggle aankan en het aantal punten dat één hit waard is. Je stelt deze waardes straks in via de Inspector.

Stap 3
Voeg een teller toe die bijhoudt hoeveel hits de Peggle al heeft gehad. Tel er één bij op wanneer de bal de Peggle raakt via OnCollisionEnter2D of OnTriggerEnter2D, afhankelijk van jouw setup.

Stap 4
Geef de score door aan de ScoreManager door vanuit het Peggle-script AddScore aan te roepen. Hierdoor zie je direct resultaat wanneer je de Peggle raakt.

Stap 5
Laat de Peggle verdwijnen wanneer de teller het ingestelde aantal hits heeft bereikt. Gebruik hiervoor Destroy(gameObject).

Stap 6
Maak de mechanic visueel door elke hit zichtbaar te maken. Dit kan bijvoorbeeld door de kleur van de Peggle donkerder te maken of door een sprite-swap te doen.

Stap 7
Test je mechanic samen met je duo-partner. Controleer of de score oploopt, of de hits worden geregistreerd en of de Peggle op het juiste moment verdwijnt.

Stap 8
Maak een GIF waarin drie dingen te zien zijn: het raken van de Peggle, het oplopen van de score en het verdwijnen van de Peggle. Voeg deze GIF toe aan je README met een korte uitleg.


---

<details>
<summary>Klik hier om de voorbeeldcode voor de Peggle te openen</summary>

```csharp

using UnityEngine;

public class Peggle : MonoBehaviour
{
    public int hitsToDestroy = 3;     // totaal aantal hits dat deze peg aankan
    public int pointsPerHit = 10;     // aantal punten dat één hit waard is


  private void OnCollisionEnter2D(Collision2D collision)
   {
        // score toekennen
        ScoreManager.Instance.AddScore(pointsPerHit);

        // aftellen
        hitsToDestroy--;

        // check of de peg nu op is
        if (hitsToDestroy <= 0)
        {
            Destroy(gameObject, 0.25f);
        }  Destroy(this.gameObject, 0.25f);
   }
}

```
</details> 







