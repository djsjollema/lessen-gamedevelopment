# Blast Galaxy Arcade Challenge – Studentenbriefing

**Introweek 2026–2027 | Game Developer × Fullstack Developer | Leerjaar 2 & 3**

---

## De opdracht

Jullie bouwen in drie dagen een compleet arcade-station voor **Blast Galaxy**, een echte arcadehal. Dat betekent drie deliverables per team:

| #   | Deliverable                                                         | Wie                  |
| --- | ------------------------------------------------------------------- | -------------------- |
| 1   | Een speelbare **arcade game**                                       | Game Developers      |
| 2   | Een **zelfgebouwde controller**                                     | Fullstack Developers |
| 3   | Een **eigen kast-opstelling** (Windows 10 pc + controller + scherm) | Fullstack Developers |

De game draait op **twee platforms**:

- De **NAMCO Noir Cabinet FHD** (arcadekast bij Blast Galaxy)
- De **eigen kast-opstelling** van jullie team op school

Beide werken via dezelfde game-executable — zonder codewijzigingen. Dat regel je met Unity's New Input System.

> **Onlosmakelijk verbonden:** zonder werkende controller is er geen eigen kast; zonder game heeft de controller niets te besturen. GD'ers en Fullstackers zijn van elkaar afhankelijk — plan en werk samen vanaf dag 1.

---

## Wat lever je op?

### 1. De game

- Gebouwd in **Unity** met het **New Input System**
- Input Action Asset met twee control schemes: `ArcadeStick` (NAMCO) en `CustomDevice` (eigen controller)
- Speelduur: 3–5 minuten per sessie (arcade-stijl: snel, pakkend)
- 1 of 2 spelers
- Bevat geluid (effecten en/of muziek)
- Draait stabiel op beide platforms

**Hardware NAMCO (houd hier rekening mee):** Windows 10, 32" 1080p, Nvidia GT 730 (geen ray tracing), DirectInput joystick.

### 2. De controller

- Origineel en zelfgebouwd — geen standaard joystick of toetsenbord
- Communiceert als **HID-gamepad** via USB of Bluetooth (Arduino Leonardo / Pro Micro of ESP32 aanbevolen)
- Robuust genoeg voor gebruik door meerdere spelers
- Gedocumenteerd: schema, componentenlijst, beknopte handleiding

### 3. De eigen kast-opstelling

- Een Windows 10 pc met je eigen controller aangesloten
- Game draait stabiel en volledig via de eigen controller
- Opstelling ziet er verzorgd uit voor de expo
- Minimaal: nette tafelopstelling met monitor, pc en controller. Ambitieus mag verder gaan.

---

## Je team

Elk team heeft ~10 studenten met vaste rollen:

| Rol                  | Profiel / Jaar    | Verantwoordelijkheid                                 |
| -------------------- | ----------------- | ---------------------------------------------------- |
| **Tech Lead**        | 3e jaar GD        | Teamleiding, GitHub, PR-reviews, stand-up leiden     |
| **Senior Game Dev**  | 3e jaar GD        | Core gameplay, Unity New Input System, dual-platform |
| **Hardware Lead**    | 3e jaar Fullstack | Controller-ontwerp, HID-firmware, documentatie       |
| **Mid Game Dev**     | 2e jaar GD        | Features, assets, UI, geluid                         |
| **Mid Hardware Dev** | 2e jaar Fullstack | Controller bouwen, kast inrichten, koppeling testen  |

---

## Planning op hoofdlijnen

| Dag               | Wat staat er centraal?                                                          |
| ----------------- | ------------------------------------------------------------------------------- |
| **Dinsdag 1/9**   | Ochtend: kennismaking. 11:15 kickoff. Middag: design sprint + technische setup. |
| **Woensdag 2/9**  | Ontwikkeldag 1 – core gameplay & controller-prototype als HID-device werkend    |
| **Donderdag 3/9** | Ontwikkeldag 2 – afronding, playtesting, code freeze 15:45                      |
| **Vrijdag 4/9**   | Expo opbouwen, jury-ronde, pitches, **finale 16:00**                            |

Elke dag start met een **stand-up** per team. Elke dag om 17:00 verplicht committen en pushen.

---

## GitHub — verplicht

Repo-naam: `gamejam-2627-gd-fs-team-XX`
Organisatie: `SoftwareDev-GameJam-2627`

**Branches:**

- `main` — alleen via PR's
- `develop` — integratiebranch
- `feature/naam` — per feature

**Per persoon minimaal:**

- 1 eigen feature branch
- 2 commits met beschrijvende berichten
- 1 pull request ingediend en goedgekeurd

**Verplichte tags:**

- `v0.1` — einde dag 1
- `v1.0.0` — code freeze donderdag 15:45

---

## Jurycriteria

De game jam telt **niet als studiecijfer**. De jury (coaches + Blast Galaxy) beoordeelt:

**Game:** speelbaarheid, arcade-gevoel, technische stabiliteit op beide platforms, creativiteit, visuals/audio, GitHub-gebruik.

**Controller:** originaliteit, werkende HID-koppeling, robuustheid, hoe goed de game erop is afgestemd, documentatie.

**Kast-opstelling:** afwerking, stabiliteit, presentatie.

---

## Prijzen

| Prijs                            | Wat win je?                                                |
| -------------------------------- | ---------------------------------------------------------- |
| **Beste game overall**           | Vrijkaartjes Blast Galaxy voor het hele team               |
| **Beste 3 games + controllers**  | Geïnstalleerd en tentoongesteld bij Blast Galaxy           |
| **Beste 2 controllers + kasten** | Komen **permanent** bij Blast Galaxy te staan              |
| **Eervolle vermeldingen**        | Meest origineel, beste samenwerking, meest ambitieus, etc. |

---

## Technische tip – Unity New Input System

```
InputActionAsset
├── Control Scheme: ArcadeStick   → NAMCO-joystick (DirectInput HID gamepad)
└── Control Scheme: CustomDevice  → eigen controller (USB/BT HID gamepad)

Acties: Move, Fire, Start — gebonden aan beide schemes.
```

Het Input System kiest automatisch het actieve apparaat. Geen `if/else` op hardwaretype nodig in je gameplay-code. Test met een standaard USB-gamepad zolang de eigen controller nog niet klaar is — de bindings zijn identiek.

---

## Wat neem je mee op dag 1?

- Laptop + oplader
- GitHub-account (al aangemaakt)
- Unity LTS geïnstalleerd incl. New Input System package
- Ideeën voor een creatieve controller (Fullstackers)
- Energie — je hebt drie dagen

---

_Blast Galaxy Arcade Challenge | Introweek 2026–2027 | Opleiding Software Developer_
