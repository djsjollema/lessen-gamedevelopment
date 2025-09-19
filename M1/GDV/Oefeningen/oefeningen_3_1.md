# Oefeningen Les 3.1: Unity Physics en Colliders  

## Werkwijze  
In deze les maak je drie **verplichte** oefeningen (3.1A, 3.1B en 3.1C).  
De *bonusuitdagingen* zijn **optioneel**: ze zijn bedoeld voor wie sneller klaar is of zichzelf extra wil uitdagen.  

De oefeningen lever je in via een **README.md** bestand op GitHub met:  
- Titel van de oefening  
- Korte omschrijving van wat je hebt gedaan  
- Een gifje met je resultaat  
- Link naar je script (indien gebruikt)  

---

## Oefening 3.1A: Vallende bal  

#### Doel  
Leer hoe je een object laat vallen en realistisch laat stuiteren met behulp van physics.  

#### Wat ga je doen?  
Je maakt een bal die door zwaartekracht naar beneden valt en stuitert op de vloer – net als een stuiterbal in *Angry Birds* of een vallend blok in *Tetris*.  

#### Stappen  
1. Voeg een vloer (met BoxCollider) en een bal (met CircleCollider) toe.  
2. Voeg een **Rigidbody** toe aan de bal.  
3. Speel de scène af en kijk hoe de bal valt.  
4. Voeg een **Physics Material** toe met bounciness > 0.  
5. Pas de bounciness aan om het verschil te zien.  

#### Bonus uitdagingen (optioneel)  
- Laat meerdere ballen tegelijk vallen met verschillende physics materials.  
- Experimenteer met gravity scale voor maan- of lood-effecten.  

---

## Oefening 3.1B: Foutieve physics  

#### Doel  
Begrijp wat er gebeurt als physics expres fout ingesteld zijn.  

#### Wat ga je doen?  
Je maakt een object dat onnatuurlijk reageert, bijvoorbeeld zweeft of extreem stuitert – alsof je een “maan-level” bouwt of een glitch in een game tegenkomt.  

#### Stappen  
1. Kopieer de scène van Oefening 3.1A.  
2. Zet gravity scale op 0 en kijk wat er gebeurt.  
3. Verander bounciness naar een extreme waarde (bijvoorbeeld 2).  
4. Observeer en noteer in je README wat er gebeurt en waarom.  

#### Bonus uitdagingen (optioneel)  
- Combineer meerdere “fouten” in één scène.  
- Maak een object dat zweeft of blijft glijden alsof het op ijs staat (lage friction).  

---

## Oefening 3.1C: Velocity en botsing  

#### Doel  
Leer hoe je een object met snelheid vooruit kunt schieten en laten botsen.  

#### Wat ga je doen?  
Je maakt een object dat met velocity beweegt en ergens tegenaan botst – vergelijkbaar met een projectiel in *Angry Birds* of een vuurbal in *Mario*.  

#### Stappen  
1. Voeg een nieuw object toe met Rigidbody en Collider.  
2. Gebruik `rigidbody.velocity = new Vector2(…);` in Start() om het een zet te geven.  
3. Plaats een muur of ander object om tegenaan te botsen.  
4. Observeer hoe de botsing verloopt.  

#### Bonus uitdagingen (optioneel)  
- Voeg meerdere muren en obstakels toe en laat je object ertegen botsen.  
- Combineer velocity met gravity voor een “projectiel-effect” (zoals een kanonskogel).  
