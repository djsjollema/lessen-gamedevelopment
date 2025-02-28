Hier is een **Mermaid flowchart** die het proces van de `SetValue(int value)` methode visualiseert.

```mermaid
flowchart TD
    A("Start public void SetValue(int value)") --> B("Set this.value = value")
    B --> C("Set tempValue = value")
    
    C --> D{"tempValue > 128?"}
    D -- Yes --> E("Set bits[7].state = true")
    E --> F("Subtract 128: tempValue -= 128")
    F --> G{"tempValue > 64?"}
    D -- No --> G

    G -- Yes --> H("Set bits[6].state = true")
    H --> I("Subtract 64: tempValue -= 64")
    I --> J{"tempValue > 32?"}
    G -- No --> J

    J -- Yes --> K("Set bits[5].state = true")
    K --> L("Subtract 32: tempValue -= 32")
    L --> M{"tempValue > 16?"}
    J -- No --> M

    M -- Yes --> N("Set bits[4].state = true")
    N --> O("Subtract 16: tempValue -= 16")
    O --> P{"tempValue > 8?"}
    M -- No --> P

    P -- Yes --> Q("Set bits[3].state = true")
    Q --> R("Subtract 8: tempValue -= 8")
    R --> S{"tempValue > 4?"}
    P -- No --> S

    S -- Yes --> T("Set bits[2].state = true")
    T --> U("Subtract 4: tempValue -= 4")
    U --> V{"tempValue > 2?"}
    S -- No --> V

    V -- Yes --> W("Set bits[1].state = true")
    W --> X("Subtract 2: tempValue -= 2")
    X --> Y{"tempValue > 1?"}
    V -- No --> Y

    Y -- Yes --> Z("Set bits[0].state = true")
    Z --> AA("Subtract 1: tempValue -= 1")
    AA --> AB("End")
    Y -- No --> AB

```

### 📌 **Uitleg van de flowchart:**
1. **Start van de methode** en initialisatie van `this.value` en `tempValue`.
2. Controle of `tempValue` groter is dan een bepaalde macht van 2 (`128, 64, 32, ..., 1`).
3. **Indien `true`**, zet de corresponderende bit op `true` en verminder `tempValue`.
4. **Indien `false`**, ga verder naar de volgende controle.
5. Herhaal dit proces voor alle 8 bits.
6. **Einde van de methode**.

🎯 **Doel:** Dit diagram helpt studenten **visueel** begrijpen hoe `SetValue(int value)` de binaire representatie instelt. Wil je nog extra verduidelijkingen of aanpassingen? 🚀