## **Lesplan: Byte Class – Een Byte opbouwen uit 8 Bits in Unity**  
**Doelgroep:** Studenten met basiskennis van Unity en C# (voortzetting van de Bit-les)  
**Duur:** 60-90 minuten  
**Leerdoelen:**  
✅ Studenten leren hoe ze **een groep objecten (bits) beheren** in een class.  
✅ Studenten begrijpen hoe ze **een array van bits** kunnen implementeren.  
✅ Studenten leren hoe ze **de binaire representatie van een byte visueel kunnen maken**.

---

## **Lesopbouw**

### **1. Introductie (10 min)**
- **Herhaling van de vorige les:**
  - Hoe werkt de **Bit** class? (kleur en interactie)
  - Hoe gebruiken we **booleans om de status te bepalen**?

- **Uitleg van het nieuwe concept:**  
  - Een **Byte** bestaat uit **8 Bits** (binaire getallenreeks).  
  - In deze les gaan we een **Byte-object maken dat 8 Bit-objecten bevat**.  
  - De Byte moet de **binaire waarde tonen en kunnen worden aangepast**.

---

### **2. Unity Scene Voorbereiden (15 min)**
1. **Maak een nieuw leeg GameObject in Unity** en noem het `ByteObject`.  
2. **Voeg het Bit-script toe** aan **8 afzonderlijke GameObjects** (maak een prefab!).  
3. **Plaats deze 8 Bits in een rij**.  
4. **Maak een nieuw C# script** en noem het **Byte.cs**.  
5. **Koppel het Byte.cs script aan het `ByteObject`.**  

---

### **3. Code Stap voor Stap Opbouwen (20-25 min)**

> **📝 Opdracht:** Studenten schrijven de code met hints.

#### **Stap 1: Byte Class maken en Bits opslaan**
**Vraag:** Hoe kunnen we 8 Bit-objecten opslaan in een array?  
👉 **Hint:** Gebruik een **array van GameObjects** of een **Bit[]**.

Laat studenten **deze code aanvullen**:

```csharp
public class Byte : MonoBehaviour
{
    public Bit[] bits = new Bit[8]; // Array om 8 Bits op te slaan

    void Start()
    {
        // Zoek alle Bit-componenten die onder deze Byte zitten
        bits = GetComponentsInChildren<Bit>();
    }
}
```

✅ **Check**: Werkt `GetComponentsInChildren<Bit>()` en vindt het alle 8 Bits?

---

#### **Stap 2: De Binaire Waarde Uitlezen**
**Vraag:** Hoe zetten we 8 booleans om in een getal?  
👉 **Hint:** Gebruik **bit shifting of een for-loop**.

Laat studenten **deze code aanvullen**:

```csharp
public int GetByteValue()
{
    int value = 0;
    for (int i = 0; i < bits.Length; i++)
    {
        if (bits[i].state)
        {
            value += 1 << (7 - i); // Bit shift voor binaire waarde
        }
    }
    return value;
}
```

✅ **Check**: Print de waarde uit in de console met `Debug.Log(GetByteValue());`

---

#### **Stap 3: Visuele Weergave van de Binaire Code**
**Vraag:** Hoe kunnen we de binaire code tonen op het scherm?  
👉 **Hint:** Gebruik een **UI Text of TMP (TextMeshPro) component**.

Laat studenten **deze code aanvullen**:

```csharp
using TMPro;

public TextMeshProUGUI binaryText;

void Update()
{
    binaryText.text = GetBinaryString();
}

string GetBinaryString()
{
    string result = "";
    for (int i = 0; i < bits.Length; i++)
    {
        result += bits[i].state ? "1" : "0";
    }
    return result;
}
```

✅ **Check**: Wordt de binaire waarde correct weergegeven in de UI?

---

### **4. Testen en Debuggen (10 min)**
- **Klik op verschillende Bits en controleer of de binaire waarde correct verandert.**  
- **Gebruik `Debug.Log(GetByteValue());` om de decimale waarde te testen.**  
- **Controleer of de UI correct wordt bijgewerkt.**  

---

### **5. Uitbreiding en Verdieping (15-20 min)**
**Extra uitdagingen:**  
🔹 **Byte aanpassen via UI:** Voeg **knoppen** toe om de Byte op "00000000" of "11111111" te zetten.  
🔹 **Decimale weergave:** Toon **zowel binaire als decimale waarde** in de UI.  
🔹 **Bit-manipulatie oefenen:** Laat de studenten **een knop maken die alle bits omzet naar hun inverse (NOT-operatie).**  

---

## **Eindresultaat**
✅ Studenten hebben een **werkende Byte class** gebouwd.  
✅ Ze kunnen **8 Bits beheren en hun binaire waarde berekenen**.  
✅ Ze hebben **visuele feedback via UI** toegevoegd.  

---
