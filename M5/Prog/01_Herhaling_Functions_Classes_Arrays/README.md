# PROG les 1: Herhaling Functions, classes en Arrays

Vorig schooljaar hebben jullie allemaal uitleg gehad over functions, classes en arrays.

Echter is het balangrijk om dit te herhalen zodat je er zeker van bent dat je dit goed begrijpt en deze principes kunt toepassen als je een game bouwt.

## Functions

Wat was ook alweer een function?

Wat is het verschil tussen een **Function** en een **Method**?

Een **Method** is een **Function** maar een **Function** niet altijd een **Method**.

Wat zijn **Parameters** en **Arguments** en hoe kunnen deze je functions flexibel maken?

Wat is een **return value** en hoe kun je hiermee je functions gebruiken om andere code te ondersteunen?

Onderzoek nog eens deze termen en check of je ze nog kent. Zo niet vraag het nog eens even aan je klasgenoten of aan je docent. Het wordt nu tijd dat je ze goed kent.

## Opdracht 1 Functions:

Maak een function **CreateBall** waarmee je een 3d bol (prefab) met een rigidbody in de scene plaatst.

```
    public GameObject prefab;
    private void CreateBall(){
        Instantiate(prefab);
    }
```

Zorg dat je deze function elke seconde aanroept zodat er elke secode een bal verschijnt en valt.

```
    private float elapsedTime = 0f;
    Update(){
        elapsedTime += Time.deltaTime;
        if(elapsedTime > 1f){
            CreateBall();
            elapsedTime = 0f;
        }
    }
```

Geef je function nu een **Paramater** voor de kleur. En zorg dat je hiermee de kleur van de material verandert.

```
    private void CreateBall(Color c){

        GameObject ball = Instantiate(prefab);
        Material material = ball.GetComponent<MeshRenderer>().material;
        material.SetColor("_Color", c);
    }
```

zorg dat je in je update random een kleur genereert die je meegeeft aan de function CreateBall() als **Argument**

```
 Update(){
        float r = Random.Range(0f,1f);
        float g = Random.Range(0f,1f);
        float b = Random.Range(0f,1f);
        Color randColor = new Color(r,g,b,1f);

        elapsedTime += Time.deltaTime;

        if(elapsedTime > 1f){
            CreateBall(randColor);
            elapsedTime = 0f;
        }

    }

```

Het resultaat is elke seconde een bal met een random kleur.

Zorg dat je bij het aanroepen van **CreateBall** ook een argument voor de position (Vector3) mee kunt geven.

Laat zo elke bal op een andere random position binnen je scherm verschijnen.

Maak een 2e function **DestroyBall** zorg dat je als argument een **Gameobject** mee kunt geven.

Zorg dat de functie het gameobject vernietigt na 3 seconden.

Laat je CreateBall een referentie naar het gameobject returnen nadat deze is aangemaakt.

Geef na het aanmaken van de bal met CreateBall de referentie door als argument in de DestroyBall function zodat de bal na 3 seconden wordt verwijderd.

```
    private GameObject CreateBall(Color c, Vector3 position){

        GameObject ball = Instantiate(prefab, position, Quaternion.identity);
        Material material = ball.GetComponent<MeshRenderer>().material;
        mat.SetColor("_Color", c);

        ...

        return ball;

    }

    Update(){
        float r = Random.Range(0f,1f);
        float g = Random.Range(0f,1f);
        float b = Random.Range(0f,1f);
        Color randColor = new Color(r,g,b,1f);

        elapsedTime += Time.deltaTime;
        if(elapsedTime > 1f){

            GameObject ball = CreateBall(randColor);
            DestroyBall(ball);

            elapsedTime = 0f;

        }

    }
```

Maak nu ook in 1 keer in je Start method 100 ballen aan met een willekeurige kleur en positie.

Dit is het eindresultaat:

![alt text](../src/01_01_balls.gif)

Maak nu ook een functie voor het genereren van een random kleur en een functie voor het genereren van een random position en gebruik deze functies in je start en update methodes. Zodat je maar op 1 plek in de code je kleur en positie hoeft te randomizen.

Je Start em Update moeten er dan ongeveer zo uitzien:

```
void Start()
{
    for (int i = 0; i < 100; i++){
        Color color = RandomColor();
        Vector3 randPos = RandomPosition(-10f, 10f);
        CreateBall(color, randPos);
    }
}

// Update is called once per frame
void Update()
{
    elapsedTime += Time.deltaTime;
    if (elapsedTime > 1f) {
        Color color = RandomColor();
        Vector3 randPos = RandomPosition(-10f, 10f);
        GameObject ball = CreateBall(color, randPos);
        DestroyBall(ball);
        elapsedTime = 0f;
    }
}
```
