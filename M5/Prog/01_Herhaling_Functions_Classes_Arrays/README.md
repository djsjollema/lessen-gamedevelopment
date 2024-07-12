# PROG les 1: Herhaling Functions, classes en Arrays

Vorig schooljaar hebben jullie allemaal uitleg gehad over functions, classes en arrays.

Echter is het balangrijk om dit te herhalen zodat je er zeker van bent dat je dit goed begrijpt en deze principes kunt toepassen als je een game bouwt.

## Functions

Wat was ook alweer een function?

Wat is het verschil tussen een **Function** en een **Method**?

Een **Method** is een **Function** maar een **Function** niet altijd een **Method**.

Wat zijn **arguments** en hoe kunnen deze je functions flexibel maken?

Wat is een **return value** en hoe kun je hiermee je functions gebruiken om andere code te ondersteunen?

## Opdracht 1a:

Maak een function **_CreateBall_** waarmee je een 3d bol met een rigidbody in de scene plaatst.

Zorg dat je de function elke seconde aanroept zodat er elke secoden een bal verschijnt en valt.

Geef je function nu een argument mee voor de kleur.

zorg dat je buiten de function random een kleur genereert die je meegeeft aan de function als **parameter**

Het resultaat is elke seconde een bal met een random kleur.

Zorg dat je bij het aanroepen van **_CreateBall_** ook een position mee kunt geven waarop de bal verschijnt.

Laat elke bal op een andere random position binnen je scherm verschijnen.

Maak een 2e function **_DestroyBall_** zorg dat je als parameter een **Gameobject** mee kunt geven.

Zorg dat de functie het gameobject vernietigd na 3 seconden.

Laat je CreateBall een referentie naar het gameobject returnen nadat deze is aangemaakt.

Geef na het aanmaken van de bal deze dus door aan de DestroyBall function zodat de bal na 3 seconden wordt verwijderd.

Maak nu ook in 1 keer 100 ballen aan met een willekeurige kleur.
