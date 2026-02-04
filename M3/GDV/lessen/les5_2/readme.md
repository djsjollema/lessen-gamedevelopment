# Les 5.2 - Animaties Creëren met Animation Window

## Leerdoelen

Na deze les kun je:

- Het Animation Window gebruiken om clips te maken
- Keyframes plaatsen en bewerken
- Sprite animaties maken voor 2D games
- Animation Events toevoegen voor timing

---

## Deel 1: Animation Window Basics (15 min)

### Animation Window Openen

1. **Window** → **Animation** → **Animation** (of Ctrl+6)
2. Selecteer een GameObject met Animator

### Interface Overzicht

```
┌───────────────────────────────────────────────────────────────────┐
│ [◄][►][●]  Clip: WalkRight ▼      │ 0:00  0:05  0:10  0:15  0:20 │
├───────────────────────────────────┼───────────────────────────────┤
│ ► Player                          │  ┆     ┆     ┆     ┆     ┆   │
│   ▼ Sprite Renderer              │  ┆     ┆     ┆     ┆     ┆   │
│       Sprite                      │  ◆─────◆─────◆─────◆─────◆   │
│   ▼ Transform                    │  ┆     ┆     ┆     ┆     ┆   │
│       Position.x                  │  ◆─────────────────────────◆   │
│       Scale                       │  ┆     ┆     ┆     ┆     ┆   │
│                                   │  ┆     ┆     ┆     ┆     ┆   │
├───────────────────────────────────┴───────────────────────────────┤
│                        [Dopesheet] [Curves]                        │
└───────────────────────────────────────────────────────────────────┘

◆ = Keyframe
[●] = Record knop
```

### Eerste Animatie Maken

1. Selecteer GameObject
2. Klik **Create** in Animation window
3. Sla op als `.anim` bestand
4. Klik op **Record** (rode cirkel)
5. Pas properties aan → keyframes worden automatisch gemaakt
6. Verplaats playhead, pas opnieuw aan
7. Stop recording

---

## Deel 2: Sprite Animation (20 min)

### Methode 1: Sprites Slepen

De snelste manier voor 2D animaties:

1. Selecteer meerdere sprites in Project window
2. Sleep ze naar het Animation window
3. Unity maakt automatisch keyframes

```
Project window:              Animation window:
┌────────────────────┐      ┌─────────────────────────────────┐
│ pacman_walk_01     │      │ Sprite: ◆───◆───◆───◆───◆───◆  │
│ pacman_walk_02     │ ───► │         01  02  03  04  05  06  │
│ pacman_walk_03     │      └─────────────────────────────────┘
│ ...                │
└────────────────────┘
```

### Methode 2: Handmatig Keyframes

1. Klik op **Record** (●)
2. Ga naar frame 0
3. Selecteer sprite in Sprite Renderer
4. Ga naar frame 5
5. Kies volgende sprite
6. Herhaal voor alle frames
7. Stop recording

### Samples (Frame Rate)

```
┌─────────────────────────────────────────────────┐
│ Samples: [12] ▼                                 │
└─────────────────────────────────────────────────┘

Samples = frames per seconde voor DEZE animatie

Voorbeelden:
12 samples = snelle animatie (game characters)
6 samples = langzame animatie (ambient objects)
24 samples = smooth animatie (cutscenes)
```

### Loop Instellen

1. Selecteer de `.anim` file in Project window
2. In Inspector: **Loop Time** ✓

---

## Deel 3: Property Animation (15 min)

### Animeerbare Properties

Bijna alles is animeerbaar:

| Component | Properties |
|-----------|------------|
| Transform | Position, Rotation, Scale |
| Sprite Renderer | Sprite, Color, Flip X/Y |
| UI Image | Color, Fill Amount |
| Camera | Size, Background Color |
| Scripts | Public variabelen! |

### Voorbeeld: Pulserende Dot

Maak een dot die pulseert om aandacht te trekken:

1. Selecteer Dot GameObject
2. Create animation: `DotPulse.anim`
3. Record mode aan
4. Frame 0: Scale = (1, 1, 1)
5. Frame 15: Scale = (1.2, 1.2, 1)
6. Frame 30: Scale = (1, 1, 1)
7. Stop recording, set Loop Time

**Resultaat:**
```
Scale.x en Scale.y over tijd:

1.2 ┤      ╱╲
    │     ╱  ╲
1.0 ┼────╱    ╲────
    │
    └────────────────►
    0   15   30  frames
```

### Voorbeeld: Color Fade

Power-up die knippert als hij bijna op is:

```
Frame 0:  Color = (1, 1, 1, 1)    // Volledig zichtbaar
Frame 5:  Color = (1, 1, 1, 0.3)  // Bijna transparant
Frame 10: Color = (1, 1, 1, 1)    // Volledig zichtbaar
```

### Curves View

Voor precieze controle over animatie timing:

1. Klik op **Curves** (onderin Animation window)
2. Selecteer een property
3. Pas de curve aan voor easing

```
Linear:          Ease In/Out:
│    ╱           │      ╭──
│   ╱            │    ╱╯
│  ╱             │  ╱
│ ╱              │ ╱
│╱               │╯
└─────           └─────
```

---

## Deel 4: Animation Events (10 min)

### Wat zijn Animation Events?

Events die een functie aanroepen op een specifiek frame:

```
Animation Timeline:
│ Frame 0      Frame 10      Frame 20 │
│    │             │             │     │
│    ▼             ▼             ▼     │
│ [Start]    [PlaySound]     [End]     │
```

### Event Toevoegen

1. Ga naar het gewenste frame
2. Rechtermuisknop op de timeline → **Add Animation Event**
3. Of: klik op het event icoon (boven de timeline)
4. Selecteer functie uit dropdown

### Event Script

```csharp
public class PacManEvents : MonoBehaviour
{
    public AudioSource audioSource;
    public AudioClip walkSound;
    public AudioClip deathSound;
    
    // Deze functies kunnen worden aangeroepen door Animation Events
    public void PlayWalkSound()
    {
        audioSource.PlayOneShot(walkSound);
    }
    
    public void PlayDeathSound()
    {
        audioSource.PlayOneShot(deathSound);
    }
    
    public void OnDeathAnimationComplete()
    {
        // Aangeroepen aan het einde van death animatie
        GameManager.Instance.RespawnPlayer();
    }
    
    // Events kunnen ook parameters meekrijgen
    public void PlaySoundWithVolume(float volume)
    {
        audioSource.volume = volume;
        audioSource.Play();
    }
}
```

### Event Parameters

| Type | Hoe | Voorbeeld |
|------|-----|-----------|
| None | Selecteer functie | `PlayWalkSound()` |
| Float | Vul waarde in inspector | `SetSpeed(0.5f)` |
| Int | Vul waarde in inspector | `SetFrame(3)` |
| String | Vul tekst in inspector | `PlaySound("step")` |
| Object | Sleep asset naar veld | `PlayClip(AudioClip)` |

---

## Oefeningen (60 min)

### Oefening 1: Pac-Man Walk Cycle (20 min)

Maak een simpele walk animatie:

1. Maak 3-4 sprite frames voor open/dicht mond
2. Maak een nieuwe animation clip `PacMan_Walk`
3. Sleep sprites naar Animation window
4. Stel Samples in op 8-12
5. Zet Loop Time aan

**Sprite frames (ASCII representatie):**
```
Frame 1:    Frame 2:    Frame 3:    Frame 2:
  ████        ███▄       ███         ███▄
 ██████      █████▄     █████▄      █████▄
██████████  █████████  ████████    █████████
 ██████      █████▀     █████▀      █████▀
  ████        ███▀       ███         ███▀

(open)      (half)     (dicht)     (half)
```

**Verwacht resultaat:**
```
Animatie loopt: mond opent en sluit continu
Frame timing: open → half → dicht → half → open...
Loop: ja
```

### Oefening 2: Ghost Hover Effect (20 min)

Maak een subtiele hover animatie voor ghosts:

1. Selecteer Ghost GameObject
2. Maak animation `Ghost_Hover`
3. Animeer Transform.Position.Y:
   - Frame 0: Y = 0
   - Frame 30: Y = 0.1
   - Frame 60: Y = 0
4. Zet loop aan

**Bonus: Voeg scale toe**
```
Frame 0:  Scale = (1.0, 1.0, 1)
Frame 30: Scale = (1.05, 0.95, 1)  // Stretch
Frame 60: Scale = (1.0, 1.0, 1)
```

**Verwacht resultaat:**
```
Position.Y over tijd:

0.1 ┤      ╱╲
    │     ╱  ╲
0.0 ┼────╱    ╲────
    │
    └────────────────►
    0   30   60  frames

Ghost beweegt langzaam op en neer (zweef effect)
```

### Oefening 3: Death Animation met Event (20 min)

1. Maak een `PacMan_Death` animatie:
   - Pac-Man draait rond
   - Pac-Man wordt kleiner
   - Fade out

2. Voeg Animation Events toe:
   - Frame 0: `PlayDeathSound()`
   - Laatste frame: `OnDeathComplete()`

3. Maak het event script

**Animatie keyframes:**
```
Frame 0:  Rotation.Z = 0,   Scale = (1, 1), Alpha = 1
Frame 30: Rotation.Z = 360, Scale = (0.8, 0.8), Alpha = 1
Frame 60: Rotation.Z = 720, Scale = (0.5, 0.5), Alpha = 0.5
Frame 90: Rotation.Z = 1080, Scale = (0, 0), Alpha = 0

Events:
├── Frame 0:  PlayDeathSound()
└── Frame 90: OnDeathComplete()
```

**Console output bij death:**
```
PlayDeathSound triggered
[90 frames later]
OnDeathComplete triggered
→ Respawning player...
```

---

## Samenvatting

### Animation Window Shortcuts

| Shortcut | Actie |
|----------|-------|
| `K` | Add keyframe |
| `Space` | Play/Pause |
| `,` / `.` | Vorig/volgend frame |
| `Shift+,` / `Shift+.` | Vorig/volgend keyframe |
| `Ctrl+A` | Select all keyframes |

### Workflow Checklist

- [ ] GameObject geselecteerd
- [ ] Animation clip gemaakt (.anim)
- [ ] Samples ingesteld (frame rate)
- [ ] Keyframes geplaatst
- [ ] Curves aangepast (optioneel)
- [ ] Loop Time ingesteld
- [ ] Animation Events toegevoegd (optioneel)
- [ ] Toegevoegd aan Animator Controller

### Tips

✅ **Doe dit:**
- Houd sprite animaties simpel (4-8 frames)
- Gebruik Animation Events voor sounds
- Preview animaties in Scene view
- Maak animaties loopable

❌ **Vermijd:**
- Te veel keyframes (wordt rommelig)
- Te snelle animaties (moeilijk te zien)
- Hardcoded timing in code (gebruik events)

---

## Volgende Les

In **Les 6.1** gaan we Game States en een Game Manager bouwen!
