Zeker! Hieronder vind je hetzelfde voorbeeld, maar dan in **C#**, waarbij een punt in poolcoördinaten wordt omgerekend naar cartesische coördinaten:

---

## 🧮 Voorbeeld in C#

```csharp
using System;

class Program
{
    static void Main()
    {
        double r = 5;
        double thetaDegrees = 45;
        double thetaRadians = thetaDegrees * Math.PI / 180; // omzetten naar radialen

        double x = r * Math.Cos(thetaRadians);
        double y = r * Math.Sin(thetaRadians);

        Console.WriteLine($"Cartesisch: ({x:F2}, {y:F2})");
    }
}
```

### ✅ Output:
```
Cartesisch: (3.54, 3.54)
```

### 🔍 Wat gebeurt er hier?

- We starten met een punt op 5 eenheden afstand en een hoek van 45 graden.
- De hoek wordt omgerekend van graden naar radialen.
- Met `Math.Cos()` en `Math.Sin()` berekenen we de x- en y-waarde.
- De output geeft ons het corresponderende cartesische punt.

---

Laat het me weten als je ook de omgekeerde berekening (van cartesisch naar pool) in C# wil zien!