# Les 3.1 Week 3 – Score & Triggers 


## Inleiding

In deze les breid je jouw Peggle-mechanic verder uit. Vorige week heb je een Peggle gemaakt die hits kan verwerken, punten doorgeeft en verdwijnt wanneer de hits op zijn. Deze week voeg je nieuwe elementen toe zoals scoreberekening, triggers en een centrale manier om events in je level te verwerken. Hiermee leg je de basis voor bonusgebieden, speciale effecten en meer geavanceerde gameplay.

---

## Theorie
Unity maakt onderscheid tussen collisions en triggers.
Een collision vindt plaats wanneer twee colliders elkaar raken en minstens één van deze colliders een Rigidbody heeft. Hierbij botsen objecten zichtbaar tegen elkaar. Een trigger werkt anders: een collider staat dan in ‘Is Trigger’-modus en zorgt niet voor fysieke botsingen, maar detecteert alleen of een object een zone binnenkomt.

Triggers worden gebruikt voor game-logica die niet afhankelijk is van fysiek gedrag, zoals scorezones, bonusgebieden, checkpoints, killzones of het starten van events. Je gebruikt OnTriggerEnter2D om te bepalen wanneer jouw bal een trigger raakt, zodat je daar een actie aan kunt koppelen, zoals punten toevoegen of een animatie starten.

Daarnaast gebruik je een centrale ScoreManager om alle punten in je spel te beheren. De ScoreManager houdt de totale score bij, verzamelt alle punten vanuit peggles en triggers en maakt het systeem overzichtelijker omdat alle scorelogica op één plek staat.

In deze les combineer je je Peggle-mechanic met triggers, zodat je straks zowel raakpunten als zones in je game kunt gebruiken om scores, states of events aan te sturen.

---


###  Voeg een GIF en uitleg toe aan je README








