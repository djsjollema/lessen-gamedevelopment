# M4 GDV Les 5 — Design Patterns: Command Pattern

## Leerdoel

Na deze les kun je:

- Uitleggen wat het Command pattern is en wanneer je het inzet
- Input-afhandeling abstraheren met Command-objecten
- Een input remapping systeem bouwen (keybindings wijzigen)
- Een undo/redo-systeem implementeren
- Commands combineren met andere patterns (Observer, Object Pool)

---

## Het probleem: Input direct koppelen aan actie

In alle voorgaande modules heb je input direct gekoppeld aan acties:

```csharp
// ❌ Directe koppeling: input → actie
void Update()
{
    if (Input.GetKeyDown(KeyCode.Space))
    {
        Jump();
    }
    if (Input.GetKeyDown(KeyCode.F))
    {
        Attack();
    }
    if (Input.GetKeyDown(KeyCode.E))
    {
        Interact();
    }
}
```

**Problemen:**

- **Keybindings wijzigen** → overal in de code aanpassen
- **Undo** is niet mogelijk → je weet niet meer wat er gedaan is
- **Replay** is niet mogelijk → acties worden niet opgeslagen
- **AI dezelfde acties laten doen** → AI kan geen toetsen indrukken

---

## De oplossing: Command Pattern

Het Command pattern **verpakt een actie in een object**. In plaats van direct een functie aan te roepen, maak je een **Command** dat de actie beschrijft.

```
Zonder Command:
  [Toets] → Jump()  (direct, niet terug te draaien)

Met Command:
  [Toets] → JumpCommand → Execute() → Jump()
                        → Undo()    → "terugdraaien"
```

> **Analogie:** Een Command is als een **bestelling in een restaurant**. De ober (input) schrijft de bestelling op een briefje (command) en geeft het aan de kok (uitvoer). Het briefje kan bewaard worden (history), aangepast worden (remap) of ongedaan gemaakt worden (undo).

### Hoe het werkt

```
┌──────────────────────────────────────────────────┐
│                Input Handler                      │
│                                                   │
│  Spatiebalk → jumpCommand.Execute()               │
│  F          → attackCommand.Execute()             │
│  E          → interactCommand.Execute()           │
│                                                   │
│  Commands zijn verwisselbaar en herkoppelbaar!    │
└──────────────────────────────────────────────────┘
         │
         ▼
┌──────────────────┐
│  Command History  │  ← Stack van uitgevoerde commands
│  [Jump, Attack]   │  → Undo: pop laatste command
└──────────────────┘
```

---

## Command Pattern stap voor stap

### Stap 1: Command interface

```csharp
public interface ICommand
{
    void Execute();
    void Undo();
}
```

> **Interface** (`ICommand`): een contract dat zegt "elke klasse die mij implementeert MOET `Execute()` en `Undo()` hebben." Het lijkt op een abstract class, maar een klasse kan meerdere interfaces implementeren.

### Stap 2: Concrete Commands

**MoveCommand.cs:**

```csharp
using UnityEngine;

public class MoveCommand : ICommand
{
    private Transform transform;
    private Vector3 direction;
    private float distance;
    private Vector3 previousPosition;  // Voor undo!

    public MoveCommand(Transform transform, Vector3 direction, float distance)
    {
        this.transform = transform;
        this.direction = direction;
        this.distance = distance;
    }

    public void Execute()
    {
        previousPosition = transform.position;  // Sla huidige positie op
        transform.position += direction * distance;
    }

    public void Undo()
    {
        transform.position = previousPosition;  // Ga terug naar vorige positie
    }
}
```

**JumpCommand.cs:**

```csharp
using UnityEngine;

public class JumpCommand : ICommand
{
    private Rigidbody2D rb;
    private float jumpForce;

    public JumpCommand(Rigidbody2D rb, float jumpForce)
    {
        this.rb = rb;
        this.jumpForce = jumpForce;
    }

    public void Execute()
    {
        rb.AddForce(Vector2.up * jumpForce, ForceMode2D.Impulse);
    }

    public void Undo()
    {
        // Sprong terugdraaien is lastig bij physics
        // In een turn-based game: reset positie
        rb.linearVelocity = Vector2.zero;
    }
}
```

**AttackCommand.cs:**

```csharp
using UnityEngine;

public class AttackCommand : ICommand
{
    private int damage;
    private GameObject target;

    public AttackCommand(int damage, GameObject target = null)
    {
        this.damage = damage;
        this.target = target;
    }

    public void Execute()
    {
        if (target != null)
        {
            Debug.Log("Attack! " + damage + " schade aan " + target.name);
            // target.GetComponent<HealthSystem>().TakeDamage(damage);
        }
        else
        {
            Debug.Log("Attack! " + damage + " schade (geen target)");
        }
    }

    public void Undo()
    {
        if (target != null)
        {
            Debug.Log("Undo attack: " + damage + " schade hersteld");
            // target.GetComponent<HealthSystem>().Heal(damage);
        }
    }
}
```

### Stap 3: Command invoeren via Input

```csharp
using System.Collections.Generic;
using UnityEngine;

public class InputHandler : MonoBehaviour
{
    [SerializeField] private float moveDistance = 1f;
    [SerializeField] private float jumpForce = 10f;

    private Rigidbody2D rb;
    private Stack<ICommand> commandHistory = new Stack<ICommand>();

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        ICommand command = null;

        // Input → Command object aanmaken
        if (Input.GetKeyDown(KeyCode.W))
            command = new MoveCommand(transform, Vector3.up, moveDistance);
        else if (Input.GetKeyDown(KeyCode.S))
            command = new MoveCommand(transform, Vector3.down, moveDistance);
        else if (Input.GetKeyDown(KeyCode.A))
            command = new MoveCommand(transform, Vector3.left, moveDistance);
        else if (Input.GetKeyDown(KeyCode.D))
            command = new MoveCommand(transform, Vector3.right, moveDistance);
        else if (Input.GetKeyDown(KeyCode.Space))
            command = new JumpCommand(rb, jumpForce);

        // Command uitvoeren en opslaan
        if (command != null)
        {
            command.Execute();
            commandHistory.Push(command);
        }

        // Undo met Z
        if (Input.GetKeyDown(KeyCode.Z) && commandHistory.Count > 0)
        {
            ICommand lastCommand = commandHistory.Pop();
            lastCommand.Undo();
            Debug.Log("Undo! Commands in history: " + commandHistory.Count);
        }
    }
}
```

---

## Input Remapping

Eén van de krachtigste toepassingen: **keybindings wijzigen** zonder code aan te passen.

```csharp
using System.Collections.Generic;
using UnityEngine;

public class RemappableInput : MonoBehaviour
{
    // Dictionary: toets → command
    private Dictionary<KeyCode, System.Func<ICommand>> keyBindings =
        new Dictionary<KeyCode, System.Func<ICommand>>();

    [SerializeField] private float moveDistance = 1f;

    void Start()
    {
        // Standaard keybindings
        SetupDefaultBindings();
    }

    void SetupDefaultBindings()
    {
        keyBindings[KeyCode.W] = () => new MoveCommand(transform, Vector3.up, moveDistance);
        keyBindings[KeyCode.S] = () => new MoveCommand(transform, Vector3.down, moveDistance);
        keyBindings[KeyCode.A] = () => new MoveCommand(transform, Vector3.left, moveDistance);
        keyBindings[KeyCode.D] = () => new MoveCommand(transform, Vector3.right, moveDistance);
    }

    // Keybinding wijzigen!
    public void RemapKey(KeyCode key, System.Func<ICommand> commandFactory)
    {
        keyBindings[key] = commandFactory;
        Debug.Log(key + " is opnieuw gekoppeld!");
    }

    void Update()
    {
        foreach (var binding in keyBindings)
        {
            if (Input.GetKeyDown(binding.Key))
            {
                ICommand command = binding.Value();  // Maak command aan
                command.Execute();
            }
        }
    }
}
```

**Voorbeeld: pijltjestoetsen in plaats van WASD:**

```csharp
// Ergens in een Settings-menu:
RemappableInput input = player.GetComponent<RemappableInput>();
input.RemapKey(KeyCode.UpArrow, () => new MoveCommand(player.transform, Vector3.up, 1f));
input.RemapKey(KeyCode.DownArrow, () => new MoveCommand(player.transform, Vector3.down, 1f));
```

---

## Undo/Redo Systeem

Met twee stacks kun je een volledig undo/redo-systeem bouwen:

```csharp
using System.Collections.Generic;
using UnityEngine;

public class UndoRedoSystem : MonoBehaviour
{
    private Stack<ICommand> undoStack = new Stack<ICommand>();
    private Stack<ICommand> redoStack = new Stack<ICommand>();

    public void ExecuteCommand(ICommand command)
    {
        command.Execute();
        undoStack.Push(command);
        redoStack.Clear();  // Na een nieuwe actie: redo-history wissen

        Debug.Log("Uitgevoerd: " + command.GetType().Name +
                  " | Undo: " + undoStack.Count +
                  " | Redo: " + redoStack.Count);
    }

    public void Undo()
    {
        if (undoStack.Count == 0)
        {
            Debug.Log("Niets om ongedaan te maken!");
            return;
        }

        ICommand command = undoStack.Pop();
        command.Undo();
        redoStack.Push(command);
    }

    public void Redo()
    {
        if (redoStack.Count == 0)
        {
            Debug.Log("Niets om opnieuw te doen!");
            return;
        }

        ICommand command = redoStack.Pop();
        command.Execute();
        undoStack.Push(command);
    }
}
```

> **Ideaal voor:** Puzzelgames, strategy games, level editors, turn-based games.

---

## Command Pattern combineren met andere patterns

### Command + Observer

Gebruik events om te melden dat een command is uitgevoerd:

```csharp
public class CommandManager : MonoBehaviour
{
    public static event System.Action<ICommand> OnCommandExecuted;
    public static event System.Action<ICommand> OnCommandUndone;

    public void Execute(ICommand command)
    {
        command.Execute();
        OnCommandExecuted?.Invoke(command);
    }

    public void UndoLast(ICommand command)
    {
        command.Undo();
        OnCommandUndone?.Invoke(command);
    }
}
```

### Command + Object Pool

Commands die vaak aangemaakt worden, kun je pooling voor gebruiken in plaats van steeds `new` aan te roepen.

---

## Wanneer Command Pattern gebruiken?

### ✅ Goed gebruik

| Situatie               | Voorbeeld                                        |
| ---------------------- | ------------------------------------------------ |
| **Undo/Redo**          | Level editors, puzzelgames, strategy games       |
| **Input remapping**    | Settings-menu met aanpasbare keybindings         |
| **Replay-systeem**     | Sla commands op, speel ze later af               |
| **AI dezelfde acties** | AI maakt dezelfde Command-objecten als de speler |
| **Turn-based games**   | Elke turn is een lijst van commands              |

### ❌ Niet nodig

| Situatie              | Waarom niet?                        |
| --------------------- | ----------------------------------- |
| **Simpele games**     | Directe input → actie is prima      |
| **Real-time physics** | Undo van physics is complex         |
| **One-way acties**    | Als je nooit hoeft terug te draaien |

---

## Oefeningen

### Oefening 1: Grid Movement met Undo

Maak een grid-gebaseerd bewegingssysteem met undo.

**Stappen:**

1. Maak de `ICommand` interface met `Execute()` en `Undo()`
2. Maak `MoveCommand` dat een transform 1 unit verplaatst in een richting
3. Maak `InputHandler` die WASD omzet naar MoveCommands
4. Houd een `Stack<ICommand>` bij als command history
5. Druk op Z om de laatste move ongedaan te maken=

**Test:**

- Beweeg het karakter met WASD over een grid
- Druk Z → karakter gaat stap voor stap terug
- Druk 5x Z → karakter is terug bij startpositie

---

### Oefening 2: Input Remapping

Maak een systeem waarmee keybindings gewijzigd kunnen worden.

**Stappen:**

1. Maak een `Dictionary<KeyCode, Func<ICommand>>` voor keybindings
2. Standaard: WASD voor beweging
3. Maak een simpele UI met knoppen om keybindings te wijzigen
4. Klik op "Remap Up" → druk een toets → die toets wordt nu "omhoog"
5. Sla de bindings op in `PlayerPrefs`

**Test:**

- Verander WASD naar pijltjestoetsen via de UI
- Herstart het spel → bindings zijn bewaard
- Alle beweging werkt nog correct met de nieuwe toetsen

---

### Oefening 3: Undo/Redo Systeem ⭐

Maak een volledig undo/redo-systeem voor een simpele level editor.

**Stappen:**

1. Maak een grid van 8×8 tiles
2. Klik op een tile om een blok te plaatsen (`PlaceBlockCommand`)
3. Klik rechts om een blok te verwijderen (`RemoveBlockCommand`)
4. Ctrl+Z = Undo, Ctrl+Y = Redo
5. Toon in de UI hoeveel undo/redo stappen beschikbaar zijn

**Test:**

- Plaats 5 blokken → Ctrl+Z 3 keer → 2 blokken over
- Ctrl+Y 2 keer → 4 blokken er weer
- Plaats een nieuw blok → redo-stack is leeg (zoals verwacht)

---

## Samenvatting

| Concept           | Uitleg                                                      |
| ----------------- | ----------------------------------------------------------- |
| Command Pattern   | Verpakt een actie in een object met `Execute()` en `Undo()` |
| `ICommand`        | Interface die elk command implementeert                     |
| Command History   | Stack van uitgevoerde commands voor undo                    |
| Input Remapping   | Keybindings wijzigen door commands te verwisselen           |
| Undo/Redo         | Twee stacks: undo-stack en redo-stack                       |
| Wanneer gebruiken | Bij undo/redo, remapping, replay of AI-input                |

---

## FAQ

**Q: Is het Command pattern niet overkill voor simpele games?**
A: Voor een simpele game waar je nooit undo nodig hebt: ja. Maar zodra je input remapping, replay of undo wilt, is het de investering waard.

**Q: Hoe werkt het Command pattern met Unity's New Input System?**
A: Het New Input System geeft je `InputAction` callbacks. In de callback maak je een Command aan en voer je het uit — de rest werkt hetzelfde.

**Q: Kan ik Commands ook via het netwerk versturen?**
A: Ja! Dit is precies hoe multiplayer turn-based games werken: elke speler stuurt Commands naar de server, de server voert ze uit en stuurt ze door.

---

## Overzicht: Alle patterns uit M4

| Les | Pattern                  | Kernidee                                            |
| --- | ------------------------ | --------------------------------------------------- |
| 1   | **Singleton**            | Eén globaal toegankelijke instance                  |
| 2   | **Object Pooling**       | Hergebruik objecten i.p.v. create/destroy           |
| 3   | **Finite State Machine** | Gedrag organiseren in states met Enter/Execute/Exit |
| 4   | **Observer**             | Losse koppeling via events (pub/sub)                |
| 5   | **Command**              | Acties verpakken in objecten (undo/redo/remap)      |

> Deze vijf patterns vormen samen een stevige basis voor professionele game-architectuur. Ze zijn combineerbaar en komen in vrijwel elke grotere game terug.
