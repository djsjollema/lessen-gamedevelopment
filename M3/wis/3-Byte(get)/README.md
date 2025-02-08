Hier is een lesplan gebaseerd op jouw originele code, zonder enige wijzigingen. De focus ligt op **begrip, analyse en experimenteren met de code in Unity**.

---

# **📚 Lesplan: Hoe werkt een byte in Unity?**
🎯 **Doelgroep:** Studenten met basiskennis van **C# en Unity**  
⏳ **Duur:** 45 - 60 minuten  
🎯 **Leerdoelen:**
- Begrijpen **wat een byte is** en hoe deze werkt in **binaire en decimale vorm**.
- **Analyseren** hoe de gegeven code een byte modelleert in Unity.
- **Experimenteren** met de code om te begrijpen hoe bits en bytes worden omgerekend.

---

## **📌 Deel 1: Introductie (10 min)**
### **Vraag aan de klas:**  
💡 *Wat is een byte? Waar worden bytes voor gebruikt?*

### **Uitleg:**  
- Een **byte** bestaat uit **8 bits**.  
- Elke **bit** kan **0** of **1** zijn.  
- Met **8 bits** kunnen waarden van **0 tot 255** worden weergegeven.  
- Computers slaan gegevens op in **binaire vorm**, omdat ze alleen met 0-en en 1-en werken.

---

## **📌 Deel 2: Analyse van de Code (15 min)**

Bekijk de volgende code:

```csharp
public class Byte : MonoBehaviour
{
    [SerializeField] Bit[] bits = new Bit[8];
    [SerializeField] private int value = 0;

    void Update()
    {
        BinToDec();
    }

    private void BinToDec()
    {
        value = 0;
        if (bits[0].state) value += 1;  // 2^0 = 1
        if (bits[1].state) value += 2;  // 2^1 = 2
        if (bits[2].state) value += 4;  // 2^2 = 4
        if (bits[3].state) value += 8;  // 2^3 = 8
        if (bits[4].state) value += 16; // 2^4 = 16
        if (bits[5].state) value += 32; // 2^5 = 32
        if (bits[6].state) value += 64; // 2^6 = 64
        if (bits[7].state) value += 128;// 2^7 = 128
    }
}
```

---

### **Vragen voor de studenten:**
1. **Wat is de rol van `bits[]` in deze code?**
2. **Wat doet de `BinToDec()` methode precies?**
3. **Waarom wordt `Update()` gebruikt om `BinToDec()` telkens aan te roepen?**
4. **Wat gebeurt er als `bits[3].state = true;` en alle andere `false` zijn?** *(Antwoord: De waarde wordt 8, omdat `bits[3]` = `2³` = 8.)*
5. **Wat is de maximale waarde die deze code kan berekenen?** *(Antwoord: 255, als alle bits op `true` staan.)*

---

## **📌 Deel 3: Code Uitvoeren en Begrijpen (15 min)**

🛠️ **Opdracht:**  
- **Open Unity en voeg de code toe in een script.**  
- **Maak een object aan met dit script en koppel het in de Inspector.**  
- **Pas handmatig enkele `Bit.state` waarden aan en bekijk wat er gebeurt met `value`.**  
- **Print de waarde in de Console (`Debug.Log(value);`).**  

🎯 **Doel:** Studenten **zien** hoe het binaire getal verandert naar een decimale waarde.

---

## **📌 Deel 4: Zelf Toepassen (20 min)**
🛠️ **Opdracht:**  
- **Experimenteer** met de code en verander **verschillende `Bit.state` waarden**.  
- **Beantwoord de volgende vragen:**
  - Wat gebeurt er als je alleen de eerste en laatste bits op `true` zet?
  - Wat gebeurt er als je alle bits **uit** zet?
  - Wat gebeurt er als je alleen `bits[4]` en `bits[6]` op `true` zet?

💡 *Tip: Gebruik de console (`Debug.Log()`) om de waarde te controleren.*

---

## **📌 Deel 5: Afronding en Bespreking (5 min)**

🎯 **Bespreek met de studenten:**
1. Hoe werkt de conversie tussen binair en decimaal in deze code?
2. Waarom zou je dit in games of software gebruiken?
3. Hoe zou je deze code uitbreiden naar een **16-bit of 32-bit systeem**?

✅ **Leerdoelen Behaald?**  
- ✅ Studenten begrijpen hoe een byte werkt.  
- ✅ Ze kunnen binaire en decimale waarden omzetten.  
- ✅ Ze hebben de code toegepast in Unity.  

🎯 **Met deze les hebben studenten niet alleen de theorie geleerd, maar ook een werkend Unity-project gebouwd waarin ze binaire getallen kunnen manipuleren! 🚀**