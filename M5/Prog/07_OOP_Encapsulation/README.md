# PROG les 7: OOP Encapsulation

Encapsulation ook wel inkapseling is een manier om je code te beschermen tegen manipulatie van buitenaf. Je kunt je vast voorstellen dat je een public value die overal vandaan aan te passen is kan leiden tot onverwachte resultaten waarna het lastig is om te bepalen waardoor dat wordt veroorzaakt.

Neem het volgende script in gedachte:

```
    class PlayerLife{
        public int life = 10;
        void Update{
            if(life == 0)Die();
        }
        void Die(){
            //player dies
            //game goes to game over screen
        }
    }
```

Elk script in mijn project wat toegang heeft tot mijn player kan van de player nu de levens instellen.
Met als gevolg dat ik dit dan ook veelvuldig doe. Mijn pickups geven me extra leven. Mijn enemies halen er leven af. Mijn kogels halen er leven af. Mijn timer doet dat ook omdat dat extra snannend is. Ook werk ik samen met andere developers die vanuit allerlij andere scripts mijn levens aan het manipuleren zijn.

Totdat mijn game ineens niet meer opstart en rechstreeks naar het gameover scherm gaat. Of wellicht kan ik juist helemaal niet meer dood omdat ergens het leven op een negatieve waarde wordt gezet. Misschien krijg ik er ineens levens bij ipv eraf omdat iemand ergens een negatieve waarde heeft afgetrokken.

Veel succes met zoeken waar er een fout gemaakt is waar begin je met zoeken?

Encapsulation zorgt ervoor dat het manipuleren van waarden niet zomaar kan en dat het gaat volgens bepaalde regels die je zelf vast kunt leggen in eigen functies.

Bijv:

```
    class PlayerLife{
        private int life = 10;
        void Update{
            if(life <= 0)Die();
        }
        public LoseLife(int amount){
            //Check of er geen vreemde hoeveelheid leven af gaat
            if(Mathf.ABS(amount) > 50)Debug.Warning("losing an unnormal amount of life");
            //forceer dat er altijd wat af gaat en nooit bij komt
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
