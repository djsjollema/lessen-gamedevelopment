# PROG les 2: Herhaling Action Events

![action](../src/02_01_action.png)

Vorig jaar hebben een aantal van jullie wellicht [deze video](https://www.youtube.com/watch?v=IKBg97A7Sbw) gezien en hiermee misschien ook zelf **Action Events** gebruikt om stukken code tussen verschillende scripts aan te roepen.

Wellicht weet je nog precies hoe je een **action event** maakt en misschien is het wel weer wat weggezakt. Hoe dan ook is het tijd om dit te herhalen of er nu voor het eerst in te duiken als je het nog niet weet.

Je kunt je ook verdiepen in [Delegates en Unity Events](https://gamedevbeginner.com/events-and-delegates-in-unity/) als het **Action Event** gesneden koek voor je is.

<a name = "action_events"></a>

## Dependancies en Tight Coupling

Wellicht ben je vorig jaar wel al in de volgende situatie beland: Je hebt een script die iets doet met **gameobject A** en een ander script op **gameobject B** wat moet weten of er iets is gebeurd met **gameobject A**. Bijvoorbeeld een UI score script dat punten moet optellen bij de score als de speler een enemy heeft verslagen. (In dit geval is er zelfs sprake van **gameobject C** , de enemy)

Nu was je oplossing waarschijnlijk om de scripts een aantal public variabelen te geven. Hieraan kon je referenties naar andere scripts meegegeven. Op die manier konden de scripts bij elkaar functies aanroepen of variabelen uitlezen of zelfs aanpassen. Deze referenties tussen classes worden ook wel **dependancies** genoemd.

Haal nu 1 van deze scripts weg en de hele boel stort als een kaartenhuis in elkaar. Zonder UI werkt je speler en enemy script niet meer en zonder enemy breekt je UI script.

Dit noemen we **"Tight Coupling"** of **"Tightley Coupled Code"**. Alles zit aan elkaar verankerd en eigenlijk werken de scripts dus samen als 1 groot script vanwege de **dependancies**!

Kijk maar eens naar dit voorbeeld:

```
Class Enemy:Monobehaviour{
    public GameObject player;
    public GameObject scoreboard;
    private int lives = 100;

    void Update(){
        FollowPlayer();
        if(lives <= 0 ){
            Die();
        }
    }
    void FollowPlayer(){
        transform.LookAt(player);
        float distance =  Vector3.Distance(player.position, transform.position);
        if(distance < 5){
            Attack(player);
        }
    }
    void Die(){
        scoreboard.AddScore(100);
    }
    void Attack(){
        //code for attack
    }
}
class Scoreboard:MonoBehaviour{
    private int score = 0;
    private TMP_Text textField;
    Start(){
        textField = GetComponent<TMP_Text>();
    }
    public void AddScore(int scoreToAdd){
        score+=scoreToAdd;
        textField.text = "score: "+score;
    }
}
```

Wat zou er nu gebeuren als je het scorebord of de speler uit het spel zou verwijderen? In het bovenstaande voorbeeld heeft de Enemy class een dependancy naar de **Player** en de **Scoreboard** classes. Ook een aanpassing in 1 van deze scripts zou tot problemen kunnen leiden. Wat zou er bijvoorbeeld gebeuren als de **AddScore** functie van de Scoreboard class private word gemaakt?

Kortom genoeg reden om te zorgen dat je deze **dependancies** en **tight couplinbg** zoveel mogelijk voorkomt.

## Action Events

Een goede manier om dependancies te voorkomen is het gebruiken van Events waarvan 1 soort event een **Action Event** is. Je hebt ook nog **Delegates** en **Unity Events** die je zou kunnen gebruiken. Waarbij **Delegates** eigenlijk de onderliggende basis vormt van de Action Events en Unity Events als voordeel hebben dat ze vanuit de inspector te koppelen zijn. Deze zijn dus makkelijk buiten de code om te gebruiken. We beperken ons nu echter tot de **Action Events**.

Een Action Event moet je eigenlijk zien als een bericht wat je kunt versturen en waar elk script naar kan luisteren of niet.

Dus bijvoorbeeld je enemies weten zelf wanneer ze dood gaan. Dat kunnen ze in hun eigen Update controleren door hun eigen lives variabele te checken.

Op het moment dat de enemy dood gaat kun je de enemy een signaal laten versturen. Zo'n signaal noemen we dus een Action Event en die moeten we eerst klaarzetten.

```
Class Enemy:Monobehaviour{
    public static event Action OnEnemyDeath; //Definitie van een Action Event
    private int lives = 100;
    void Update(){
        if(lives <= 0 ){
            Die();
        }
    }
}

```

Het Action Event is zowel **public** als **static**. Static betekent dat deze variabele vanuit elk ander script direct te benaderen is via de class Enemy die niet geinstantieerd is. Echter kan er dus maar 1 versie van deze variabele bestaan ook al zijn er meer enemies. Hier wordt het dus ook gelijk duidelijk waarom het belangrijk is om Classes Uppercase te schrijven en variabelen lowercase.

```
    Enemy.OnEnemyDeath //zo benader je vanuit een ander script een static variabele
```

Op het moment dat de enemy dood gaat laten we hem nu het event versturen. Dit doen we met de **Invoke** functie:

```
Class Enemy:Monobehaviour{
    public static event Action OnEnemyDeath; //Definitie van een Action Event
    private int lives = 100;
    void Update(){
        if(lives <= 0 ){
            Die();
            OnEnemyDeath?.Invoke();
        }
    }
}
```

_Sidenote:
Eigenlijk is het technisch gezien zo dat er geen bericht verstuurd wordt maar dat er wordt gekeken of er functies opgeslagen zitten in het Action Event. Als je dit echt goed wil begrijpen moet je onderzoeken hoe [Delegates](https://gamedevbeginner.com/events-and-delegates-in-unity/) werken. Maar voor de begrijpelijkheid houden we even het idee van een bericht versturen vast._

Er wordt een bericht gestuurd als er een enemy dood gaat maar niemand luistert daar nog naar.

Om te zorgen dat andere scripts hier naar gaan luisteren gaan we ons in de Start methode van deze scripts "abboneren" op deze berichten. Dit doen we door een functie te maken die we met **+=** gaan toevoegen aan de Action. Let op dat je geen () achter de naam van de functie zet.

```
class Scoreboard:MonoBehaviour{
    private int score = 0;
    private TMP_Text textField;
    Start(){
        textField = GetComponent<TMP_Text>();
        Enemy.OnEnemyDeath += GetEnemyPoints;   //We "abboneren" ons op het Action Event
    }
    private void GetEnemyPoints(){              //Als het bericht binnenkomt dat de enemy dood is voeren we de functie uit
        score += 100;
        textField.text = "score: "+score;
    }
}
```

Ik heb nu een script dat mijn score verhoogt als er een enemy dood gaat.

Als ik geen enemies meer heb doet mijn Scoreboard script het nogsteeds prima. Het script wacht wel op een bericht wat nooit komt maar dat maakt niet uit.

Ook al verwijder ik nu mijn Scoreboard uit mijn game zullen mijn enemies gewoon berichten blijven sturen als ze dood gaan. er is gewoon geen Scoreboard meer wat daar naar luistert en vervolgens iets doet.

Je kunt zoveel scripts laten luisteren naar een Action Event als je wil en dat zal nooit een probleem opleveren.

Met de onderstaande code kun je er ook voor zorgen dat een script stopt met luiteren naar een event:

```
    Enemy.OnEnemyDeath -= GetEnemyPoints;
```

<a name = "opdracht1"></a>

### Opdracht 4 Action Events

Maak op een canvas een gameobject genaamd scoreboard met een textfield (TMPro) aan waar je score in gaat bijhouden.

Hang aan je scoreboard een script met de classname **Scoreboard**.

Maak een blokje waarmee je door een level rond kunt lopen met WASD.

Maak een prefab voor een pickup en hang hieraan een script met als classname **Pickup** die checkt of hij geraakt wordt door de player.

Laat de **Pickup** een Action Event versturen als hij is opgepakt.

Laat het **Scorebord** luisteren naar het bericht en een score van **50** punten optellen en tonen in het tekstveld van het scoreboard.

![Het Resultaat](../src/02_02_result.gif)

Klaar met de opdracht?

- **_Push je code naar github en maak een screen capture van je werkende prototype._**
- **_Lever een link je code en je gifje in via educator._**

### Bonus

Zoek uit hoe je aan het Action Event data zoals bijvoorbeeld een integer mee kunt geven.
Zorg dat elke pickup een andere score geeft dat via het event wordt meegegeven en zo in de UI bij de score wordt opgeteld.

![Het Resultaat](../src/02_03_result_bonus.gif)
