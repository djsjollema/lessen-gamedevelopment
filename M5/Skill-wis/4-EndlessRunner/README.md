# Endless Runner

# De opdracht
![EndlessKitty](images/endlessRunner.gif)

# uitvoering
## stap 1 keuze karakter
download een karakter van www.mixamo.com

bijvoorbeeld Claire
<img src="images/claire.png">

Maak een map `Models' en plaats het 'fbx'-bestand (Filmbox) daar 


## stap 2 keuze animaties
download voor jouw karakter een animate van een run

<img src="images/claireRunning.gif">

download voor jouw karakter een animatie van een jump

<img src="images/claireJumping.gif">


importeer de animaties via de dialoogbox en dupliceer met ctrl-d de uiteindelijke animaties

## stap 3 maak een Animator

Maak een nieuwe Animator en zet de 'run' als default en maak een transitie van de 'jump' terug naar de 'run'

<img src="images/animator.png">

## Stap 4 Plaats in de Hierarchy

Maak een nieuwe scene-2d en plaats het model van Clair in de Hierarchy.

Voeg jouw Animator toe als een component van Claire

## Stap 5 script
Voeg aan Claire ook een script "endlessRunner" met de volgende variabelen

```` cs
    [SerializeField] float vbegin = 4;
    [SerializeField] float g = -5;
    Animator animator;

    enum State { running, jumping};
    State myState = State.running;

    Vector3 velocity = Vector3.zero;
    Vector3 acceleration = Vector3.zero;

    float tmax = 1.667f;
    float t = 0;
````

Ontwikkel een script met:
* in de Start initiatie van de Animator
* in de Upload een gameloop waarbij de velocity en positie van Clair worden vastgesteld
* in de Upload een state-machine waar de toestanden `running` en `jumping` worden vastgelegd 
