# PROG les 7: OOP Encapsulation

"Encapsulation", ook wel "inkapseling" in het nederlands, is een manier om je code te beschermen tegen manipulatie van buitenaf. Je kunt je vast voorstellen dat je een public value die overal vandaan aan te passen is kan leiden tot onverwachte resultaten, waarna het lastig is om te bepalen waardoor dat wordt veroorzaakt.

Neem het volgende script in gedachten , wat op een player gameobject zit:

```
    class PlayerLife:MonoBehaviour{
        public int life = 10;
        void Update{
            if(life <= 0)Die();
        }
        void Die(){
            //player dies
            //game goes to game over screen
        }
    }
```

Elk script in het project wat toegang heeft tot mijn player, kan van de player nu de levens instellen.
Met gevolgen als ik dit veelvuldig doe. Mijn pickups geven me extra leven. Mijn enemies halen er leven af. Mijn kogels halen er leven af. Mijn timer doet dat ook omdat dat extra snannend is. Ook werk ik samen met andere developers die vanuit allerlei andere scripts mijn levens aan het manipuleren (uitlezen en aanpassen) zijn.

Tot ineens blijkt dat mijn game niet meer opstart en rechstreeks naar het gameover scherm gaat. Of wellicht kan ik juist helemaal niet meer dood omdanks dat ik al 1000 x geraakt ben. Misschien krijg ik er ineens levens bij i.p.v eraf wanneer ik word geraakt.

Veel succes met zoeken waar er een fout gemaakt is waar begin je met zoeken?

Encapsulation betekent dat je je code afschermt om aangepast te worden en dat je deze alleen als het niet anders kan op een zo veilig mogelijke manier beschikbaar maakt.

## Methods

Bijvoorbeeld voor dit in een method(function) te doen zodat je kunt afdwingen dat het volgens een aantal regels gaat:

```
    class PlayerLife{
        private int life = 10;
        public LoseLife(int amount){
            //Check of er geen vreemde hoeveelheid leven af gaat
            if(Mathf.ABS(amount) > 50)Debug.LogWarning("losing an extreme amount of life");
            //forceer dat er altijd wat af gaat en nooit per ongeluk iets bij komt
            life -= Mathf.ABS(amount);
            if(life <= 0){
                Die();
            }
        }
        void Die(){
            //player dies
            //game goes to game over screen
        }
    }
```

_Een bijkomend voordeel van de bovenstaande code is ook dat er niet meer elk frame gecontroleerd hoeft te worden hoeveel levens de speler nog heeft en alleen nog maar als er een leven vanaf gaat. Dat bespaart weer een hoop processor kracht._

## Getter & Setter

Je kunt ook werken met zogenaamde **"getters"** en **"setters"**. Dit zijn eigenlijk ook methoden waar je extra checks in kunt zetten die je bovendien ook de mogelijkheid geven om variabelen alleen leesbaar of alleen schrijfbaar te maken.

Het leuke van **Getters** en **Setters** is ook dat ze buiten de class worden behandeld als property (variable) in plaats van als methode.

![getter setter](../src/07_01_getter_setter.png)

Dankzij de code die je in de getter en setter plaatst kun je mogelijke fouten van mededevelopers opvangen:

![mistake](../src/07_02_max_lives.png)
![negative](../src/07_03_neg_lives.png)

Je hoeft geen code te implementeren in een getter en een setter. Je kunt ze ook leeg laten. Dan is de property gewoon beschikbaar om te lezen en te schrijven.

![no code](../src/07_04_getter_setter_no_code.png)

Je kunt ook alleen de **getter** implementeren wat resulteert in een **read-only** property.
![read-only](../src/07_05_readonly.png)
Je krijgt dan een error als je iets probeert weg te schrijven.
![read_only_error](../src/07_07_readonly_error.png)

Je mag er ook een **write-only** property van maken. Door alleen de **setter** te gebruiken. Maar dan kun je er dus niets uit opvragen.

![write_only](../src/07_06_writeonly.png)
![write_only_error](../src/07_08_writeonly_error.png)

Alleen iets wegschrijven lukt dan dus wel.
![write_only_succes](../src/07_09_writeonly_succes.png)

Getters en Setters gebruiken is een goede manier om waarden van variabelen dus op een gecontroleerde manier zo beperkt mogelijk beschikbaar te maken voor andere scripts.

### Opdracht 1:

Ga door je towerdefense project heen en zoek op hoeveel public variables je hebt gebruikt. Vervang deze **allemaal** met een getter en/of setter.

**Write only:**
Als je vanuit een ander script alleen wegschrijft maak je er een **setter** van.

**Read only:**
Als je vanuit een ander script alleen leest maak je er een **getter** van.

**Read write:**
En als je vanuit een ander script zowel leest als schrijft implementeer je de **getter** en de **setter**.

Bedenk nu of er waarden zijn
