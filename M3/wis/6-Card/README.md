## **Lesopzet: Een Kaartklasse Implementeren in Unity**

### **Lesdoelen**
Na deze les kunnen studenten:
1. **Begrijpen** hoe een kaartobject wordt geprogrammeerd in Unity.
2. **Declareren en gebruiken** van variabelen binnen een Unity C#-script.
3. **Werken met SpriteRenderer** om sprites te tonen en wisselen.
4. **Gebruiken van MonoBehaviour-methoden** zoals `Start()`, `Update()` en `OnMouseUp()`.
5. **Maken van een flip-mechanisme** waarmee een kaart omgedraaid kan worden met een muisklik.

---

## **Lesstructuur**
| Tijd | Activiteit | Doel |
|------|------------|------|
| **5 min** | Introductie: Wat gaan we maken? | Context en leerdoelen uitleggen |
| **10 min** | Opzetten van een nieuwe Unity-scene en objecten | Basis Unity-omgeving klaarzetten |
| **15 min** | Stapsgewijs implementeren van de `Card`-klasse | Code stap voor stap opbouwen en uitleggen |
| **10 min** | Testen en debuggen | Functionaliteit controleren en problemen oplossen |
| **5 min** | Uitbreiding en reflectie | Extra uitdagingen geven en code bespreken |

---

## **1. Introductie (5 min)**
- **Wat gaan we bouwen?**  
  We maken een speelkaart die kan worden omgedraaid bij een muisklik. De kaart heeft een voor- en achterkant en toont informatie over de rang en suit wanneer erop wordt geklikt.

- **Concepten die we behandelen:**
  - Werken met **Sprites** en de **SpriteRenderer**.
  - Gebruik van **public en private variabelen** in C#.
  - **MonoBehaviour-methoden** zoals `Start()`, `Update()` en `OnMouseUp()`.
  - **Interactie met de speler** via muisklikken.

**Vraag aan de studenten:** *Welke methoden verwacht je dat belangrijk zijn om een interactief kaartobject te maken?*

---

## **2. Opzetten van de Unity Scene en Objecten (10 min)**

1. **Open Unity en maak een nieuw 2D-project.**  
   - Voeg een leeg GameObject toe en noem het "Card".
   - Voeg een **SpriteRenderer** component toe.
   - Voeg een **BoxCollider2D** toe zodat we interactie kunnen detecteren.

2. **Sprites importeren en toewijzen**  
   - Voeg twee sprite-afbeeldingen toe: een **voorkant** en een **achterkant**.
   - Wijs een willekeurige afbeelding toe aan de **SpriteRenderer**.

3. **Maak een nieuw script en noem het `Card.cs`**  
   - Open het script in Visual Studio Code of een andere code-editor.

---

## **3. Stapsgewijze Implementatie van de `Card`-klasse (15 min)**

**Stap 1: De Klasse Structuur Opzetten**
```csharp
using UnityEngine;

public class Card : MonoBehaviour
{
    public Sprite Front;
    [SerializeField] Sprite Back;
    bool visible = false;
    SpriteRenderer spriteRenderer;
    public string rank;
    public string suit;
}
```
- **Uitleg:**  
  - `Front`: Publieke variabele zodat we in de Unity-editor een sprite kunnen toewijzen.  
  - `Back`: Een `[SerializeField]` variabele, privé maar zichtbaar in de editor.  
  - `visible`: Houdt bij of de kaart zichtbaar is of niet.  
  - `spriteRenderer`: Verwijzing naar de SpriteRenderer-component.  
  - `rank` en `suit`: Strings om kaartinformatie op te slaan.

**Vraag aan de klas:** *Waarom is de `Back` sprite privé met `[SerializeField]`, maar `Front` publiek?*

---

**Stap 2: De `Start()` Methode Implementeren**
```csharp
void Start()
{
    spriteRenderer = GetComponent<SpriteRenderer>();
    spriteRenderer.sprite = Back;
}
```
- **Uitleg:**  
  - `GetComponent<SpriteRenderer>()` haalt de SpriteRenderer op die gekoppeld is aan de kaart.
  - De sprite wordt standaard op de achterkant ingesteld.

---

**Stap 3: De `Update()` Methode voor Weergave van Sprites**
```csharp
void Update()
{
    if (visible)
    {
        spriteRenderer.sprite = Front;
    }
    else
    {
        spriteRenderer.sprite = Back;
    }
}
```
- **Uitleg:**  
  - Dit controleert **elke frame** of `visible` waar of onwaar is.
  - De juiste sprite wordt getoond op basis van de status van `visible`.

---

**Stap 4: De `OnMouseUp()` Methode Voor Interactie**
```csharp
public void OnMouseUp()
{
    flip();
}
```
- **Uitleg:**  
  - `OnMouseUp()` is een ingebouwde Unity-methode die wordt aangeroepen wanneer de speler **de muisknop loslaat op het object**.
  - Dit zorgt ervoor dat de kaart reageert op kliks.

---

**Stap 5: De `flip()` Methode Implementeren**
```csharp
public void flip()
{
    visible = !visible;
    print(suit + " " + rank);
}
```
- **Uitleg:**  
  - `visible = !visible;` verandert de waarde (true wordt false en andersom).
  - De `print()`-functie toont de suit en rank in de **Console**, zodat we kunnen zien welke kaart is omgedraaid.

---

## **4. Testen en Debuggen (10 min)**
1. **Sleep het `Card.cs` script naar het "Card" GameObject in Unity.**
2. **Wijs een sprite toe voor `Front` en `Back` in de Inspector.**
3. **Voeg een `BoxCollider2D` toe aan de kaart (indien nog niet gedaan).**
4. **Klik op "Play" en test of de kaart omdraait bij een muisklik.**
5. **Bekijk de console-output om te controleren of `suit` en `rank` correct worden weergegeven.**

**Vraag aan de studenten:**  
*Wat gebeurt er als je meerdere keren klikt? Hoe werkt de `flip()` methode precies?*

---

## **5. Uitbreiding en Reflectie (5 min)**
### **Mogelijke uitbreidingen**
- **Voeg een animatie toe bij het omdraaien van de kaart.**
- **Laat meerdere kaarten in een spel werken en bepaal regels.**
- **Gebruik geluidseffecten bij het omdraaien.**

### **Reflectievragen**
1. *Welke rol speelt de SpriteRenderer in dit script?*
2. *Waarom gebruiken we `Update()` in plaats van direct de sprite te veranderen in `flip()`?*
3. *Welke alternatieve methoden zouden we kunnen gebruiken om een kaart om te draaien?*

---

## **Eindresultaat**
Na deze les hebben studenten:
✅ Een werkende `Card`-klasse geprogrammeerd in Unity.  
✅ Begrip van hoe sprites werken met `SpriteRenderer`.  
✅ Geleerd hoe je muisklikken detecteert en gebruikt in C#.  
✅ De mogelijkheid om het script uit te breiden met extra functies.

---

### **Bonus Oefening**
**Laat studenten samenwerken en een eenvoudig kaartspel maken.**  
Bijvoorbeeld: als twee kaarten met dezelfde suit worden omgedraaid, blijven ze zichtbaar.

---

Met deze lesopzet leren studenten niet alleen hoe ze een interactief kaartobject maken in Unity, maar krijgen ze ook inzicht in **game mechanics, interactie en debugging**. 🚀