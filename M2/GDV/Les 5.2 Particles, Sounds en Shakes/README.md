# M2 GDV les 5.2 (CODE) Particles , Sounds & Shakes

Deze les maken jullie kennis met particle effecten in unity. We gaan ook geluiden toevoegen en afspelen en tot slot programmeren we een lekkere screenshake, onmisbaar voor een goed gevoel tijdens het gamen.

## Particle System

In Unity kun je als component een Particle System toevoegen aan je gameobjecten.

![particle system](../src/5_2_particle%20system.gif)

Het maken van mooie visuele effecten met particles is het werk van game artists. Maar ook met een beetje moeite kun je als game developer hier iets leuks van maken.

Het 'explosie effectje' kun je namaken door aan een gameobject een `ParticleSystem` component te hangen.

De specifieke settings voor dit effect kun je in de screenshots terugzien:

![](/M2/GDV/src/5_2_particle_settings_1.png)
![](/M2/GDV/src/5_2_particle_settings_2.png)
![](/M2/GDV/src/5_2_particle_settings_3.png)
![](/M2/GDV/src/5_2_particle_settings_4.png)
![](/M2/GDV/src/5_2_particle_settings_5.png)

Probeer zelf ook eens een beetje te spelen met de settings om het effect eigen te maken.

Je hebt nu ook code nodig om je particles te activeren. Dit doen we in het script `BumperHit.cs`.

```csharp
using System;
using UnityEngine;

public class HitBumper : MonoBehaviour
{

    [SerializeField] private int bumperValue = 50;

    //maak een variabele voor je Particle System aan
    private ParticleSystem ps;

    public static event Action<Transform,int> onHitBumper;
    private void Start()
    {
        //sla je Particle System op in je variabele zodat je er later dingen mee kunt doen
        ps = GetComponent<ParticleSystem>();

        //zet hem stil!
        ps?.Stop();
    }
    private void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Ball")) {

            onHitBumper?.Invoke(gameObject.transform, bumperValue);
            //zet hem eerst weer stil voor het geval hij nog niet klaar was
            ps?.Stop();
            //speel hem nu af
            ps?.Play();
        }
    }
}


```

## Audio & Sounds

### Geluid importeren

Om geluid in Unity te gebruiken, plaats je je audio-bestanden (`.mp3`, `.wav`, `.ogg`) in de `Assets` folder van je project. Unity detecteert deze automatisch. De audio-files verschijnen dan in je Project window waar je ze kunt selecteren en gebruiken.

### AudioSource Component

Om geluid af te spelen, moet je een `AudioSource` component aan je GameObject toevoegen:

1. Selecteer het GameObject in de Hierarchy
2. Klik op `Add Component` in de Inspector
3. Zoek naar `AudioSource` en voeg deze toe
4. Sleep je audio-bestand in het `AudioClip` veld van de AudioSource
5. **Belangrijk:** Zet `Play on Awake` uit in de Inspector

De `Play on Awake` optie zorgt ervoor dat het geluid automatisch afgespeeld wordt wanneer je game start. Dit willen we voorkomen omdat we het geluid vanuit code willen besturen. Zorg dat deze checkbox **uitgevinkt** is.

### Geluid afspelen vanuit code

Je kunt geluid afspelen met de `Play()` methode van de AudioSource. Hier is een voorbeeld:

```csharp
using UnityEngine;

public class SoundManager : MonoBehaviour
{
    private AudioSource audioSource;

    void Start()
    {
        audioSource = GetComponent<AudioSource>();
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            audioSource.Play();
        }
    }
}
```

**Waarom GetComponent()?**

In plaats van handmatig de AudioSource in te stellen via de Inspector, haal je deze op met `GetComponent<AudioSource>()`. Dit zoekt automatisch naar het AudioSource component op hetzelfde GameObject. Dit is schoner en je hoeft geen variabelen handmatig in de Inspector in te vullen.

Zet dit script op hetzelfde GameObject als je AudioSource. Nu zal het geluid afspelen wanneer je op Spatie drukt.

Je kunt ook `PlayOneShot()` gebruiken voor korte effectgeluiden, of `Stop()` om geluid te stoppen.

**Probeer nu zelf eens goed na te denken hoe je nu je geluidje kunt afspelen zodra je bal een bumper raakt!**

Tip: Denk aan de [Action events uit les 4.2](../Les%204.2%20Scores%20versturen/README.md)

---

## Opdracht: Particles & Sound effect

Voeg met behulp van de bovenstaande uitleg particles en geluiden toe aan je bumpers als de bal deze raakt.

## Inleveren op je README

Zet in de titel **5.2 Particles & Sound effect**
Maak een korte omschrijving en GIF van je prototype en zet deze op je readme. Zet hier ook de links naar de code.

## Extra: Screenshake

Zorg ook dat het scherm gaat schudden als de bal de bumper raakt.

## Screen Shake

![](https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExd3B3MzhtYWQxY2p1eHh4amx1d2hkbWo0aWx3dzRvYWh5bmdteHFpeSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/26H73Dl4HXXFe/giphy.gif)

Screen Shake geeft je spel meer impact en feedback wanneer belangrijke gebeurtenissen plaatsvinden, zoals explosies of hits.

### De ScreenShake code

```csharp
using System.Collections;
using UnityEngine;

public class Screenshake : MonoBehaviour
{
    // Originele positie van de camera (start positie)
    private Vector3 origin;
    // Hoelang de shake effect duurt in seconden
    private float shakeTime;
    // Hoe sterk/ver de camera beweegt
    private float shakeForce;
    // Telt hoe veel tijd is verstreken sinds de shake begon
    private float elapsedTime = 0f;

    void Start()
    {
        // Sla de originele positie op
        origin = transform.position;
        // Luister naar events van andere scripts
        HitBumper.onHitBumper += ShakeBumper;
    }

    // Verwijder event listeners wanneer dit script uitgeschakeld wordt
    private void OnDisable()
    {
        HitBumper.onHitBumper -= ShakeBumper;
    }

    // Wordt aangeroepen wanneer de bumper geraakt wordt
    private void ShakeBumper(Transform _, int points) {
        shakeTime = .1f;      // Korte shake: 0.1 seconde
        shakeForce = .04f;    // Kleine amplitude
        elapsedTime = 0f;     // Reset de timer
        StopCoroutine("TrembleStep");  // Stop eventueel lopende shake
        StartCoroutine("TrembleStep");
    }
    // Coroutine die de camera aan het trillen zet
    private IEnumerator TrembleStep() {
        // Blijf trillen zolang we nog tijd over hebben
        while (elapsedTime < shakeTime)
        {
            // Verplaats de camera naar een willekeurige positie rond de origineel
            transform.position = new Vector3(
                origin.x + Random.Range(-shakeForce, shakeForce),  // Random x
                origin.y + Random.Range(-shakeForce, shakeForce),  // Random y
                origin.z                                            // Z blijft hetzelfde
            );
            // Update de verstreken tijd in de coroutine
            elapsedTime += Time.deltaTime;
            // Wacht tot volgende frame
            yield return new WaitForEndOfFrame();
        }
        // Zet de camera terug op de originele positie
        transform.position = origin;
    }
}
```

### Hoe werkt deze code?

**Events en callbacks:** De code luistert naar twee events: `onHitBumper` en `onComboAchieved`. Wanneer deze events plaatsvinden, wordt de `ShakeBumper()` methode automatisch aangeroepen.

**Shake parameters:** Elk event stelt verschillende parameters in:

- `shakeTime`: hoe lang de shake duurt
- `shakeForce`: hoe sterk de camera beweegt (amplitude)
- `elapsedTime`: houdt bij hoeveel tijd is verstreken

**StopCoroutine:** Voordat een nieuwe shake begint, wordt de vorige shake gestopt met `StopCoroutine("TrembleStep")`. Dit zorgt ervoor dat overlappende effects netjes worden afgehandeld en geen conflicten ontstaan.

**De TrembleStep coroutine:** Dit is de kern van het effect:

1. De loop herhaalt zich zolang `elapsedTime < shakeTime`
2. Elke frame wordt de camera naar een willekeurige positie verplaatst rond de originele positie
3. `Random.Range(-shakeForce, shakeForce)` zorgt voor random beweging in x en y
4. **`elapsedTime` wordt in de coroutine zelf geupdate**, niet in `Update()`. Dit voorkomt timing bugs die kunnen ontstaan wanneer meerdere shake effects tegelijk werken
5. `yield return new WaitForEndOfFrame()` pauzeert de coroutine tot de volgende frame
6. Na afloop gaat de camera terug naar de originele positie

Voeg deze code nu toe aan je camera!
