# Les 01 – Herhaling: Variabelen, Functies, Classes en Arrays

## Theorie

### Variabelen

Een variabele slaat een waarde op onder een naam. Je geeft altijd het **type** aan.

```csharp
int score = 10;
string naam = "Speler1";
bool leeft = true;
```

Veelgebruikte types: `int` (geheel getal), `float` (decimaal), `string` (tekst), `bool` (waar/niet-waar).

#### Overzicht veelgebruikte datatypes

| Type | Omschrijving | Voorbeeld |
|------|-------------|-----------|
| `int` | Geheel getal (32-bit) | `int score = 42;` |
| `float` | Decimaal getal (32-bit, ~7 cijfers) | `float snelheid = 3.5f;` |
| `double` | Decimaal getal (64-bit, ~15 cijfers) | `double afstand = 1.234567890;` |
| `bool` | Waar of niet-waar | `bool isActief = true;` |
| `string` | Tekst (reeks tekens) | `string naam = "Speler";` |
| `char` | Eén enkel teken | `char letter = 'A';` |
| `long` | Groot geheel getal (64-bit) | `long punten = 9999999999L;` |
| `byte` | Klein geheel getal (0–255) | `byte niveau = 3;` |
| `uint` | Positief geheel getal (0–4 miljard) | `uint stappen = 100000u;` |
| `Vector2` | 2D-positie (Unity) | `Vector2 pos = new Vector2(1f, 2f);` |
| `Vector3` | 3D-positie (Unity) | `Vector3 pos = new Vector3(0f, 1f, 0f);` |

---

### Functies

Een functie is een herbruikbaar stuk code. Je geeft aan wat hij **teruggeeft** en welke **parameters** hij nodig heeft.

```csharp
int Optellen(int a, int b)
{
    return a + b;
}

int resultaat = Optellen(3, 5); // resultaat = 8
```

Gebruik `void` als de functie niets teruggeeft.

---

### Classes

Een class is een **blauwdruk** voor een object. Een object is een instantie van die class.

```csharp
class Vijand
{
    public string Naam;
    public int HP;

    public void Aanval()
    {
        Console.WriteLine(Naam + " valt aan!");
    }
}

Vijand v = new Vijand();
v.Naam = "Goblin";
v.HP = 50;
v.Aanval();
```

---

### Arrays

Een array slaat meerdere waarden van hetzelfde type op in één variabele.

```csharp
int[] scores = new int[3];
scores[0] = 10;
scores[1] = 20;
scores[2] = 30;

// Of direct initialiseren:
string[] namen = { "Alice", "Bob", "Charlie" };

// Doorlopen met een lus:
for (int i = 0; i < namen.Length; i++)
{
    Console.WriteLine(namen[i]);
}
```

---

## Oefeningen

---

### Oefening 1 – Variabelen: Spelersnaam en Score

Maak drie variabelen aan:

- een `string` voor de naam van de speler
- een `int` voor de score
- een `bool` die bijhoudt of de speler nog leeft

Print de waarden naar de console.

```csharp
// Jouw code hier
```

---

### Oefening 2 – Variabelen: Berekening met HP

De speler heeft 100 HP. Hij wordt geraakt voor 35 schade. Bereken de resterende HP en druk die af.  
Gebruik daarna een tweede aanval van 80 schade. Druk af of de speler nog leeft (`HP > 0`).

```csharp
// Jouw code hier
```

---

### Oefening 3 – Functies: Begroeting

Schrijf een functie `Begroet(string naam)` die "Welkom, [naam]!" afdrukt.  
Roep de functie aan met je eigen naam.

```csharp
// Jouw code hier
```

---

### Oefening 4 – Functies: Max van twee getallen

Schrijf een functie `int Max(int a, int b)` die het grootste van twee getallen teruggeeft.  
Test de functie met een paar waarden en druk het resultaat af.

```csharp
// Jouw code hier
```

---

### Oefening 5 – Functies: Schade berekenen

Schrijf een functie `int BerekenSchade(int aanval, int verdediging)` die `aanval - verdediging` teruggeeft (minimaal 0).  
Roep de functie aan en druk de schade af.

```csharp
// Jouw code hier
```

---

### Oefening 6 – Arrays: Vijanden

Maak een array van vijf vijandnamen (strings).  
Druk alle namen af met een `for`-lus.

```csharp
// Jouw code hier
```

---

### Oefening 7 – Arrays: Hoogste score

Maak een array van vijf scores (integers).  
Schrijf code die de hoogste score vindt en afdrukt.

```csharp
// Jouw code hier
```

---

### Oefening 8 – Classes: Speler

Maak een class `Speler` met de volgende velden:

- `string Naam`
- `int HP`
- `int Score`

Maak een object aan, vul de velden in en druk ze af.

```csharp
// Jouw code hier
```

---

### Oefening 9 – Classes: Methode toevoegen

Breid de `Speler`-class uit met een methode `Vertel()` die een zin naar de console schrijft zoals:  
`"Ik ben [Naam], mijn HP is [HP] en mijn score is [Score]."`

Roep de methode aan.

```csharp
// Jouw code hier
```

---

### Oefening 10 – Combinatie: Array van Spelers

Maak een array van drie `Speler`-objecten. Geef elk een naam, HP en score.  
Schrijf een functie `DrukSpelersAf(Speler[] spelers)` die voor elke speler `Vertel()` aanroept.

```csharp
// Jouw code hier
```
