# Lesplan M4 Programmeren

Tijdens de modulen M1 PROG en M2 PROG hebben jullie de basisvaardigeden voor het programmeren behandeld in het [**.NET** framework.](https://dotnet.microsoft.com/en-us/)

Deze programmeer basisvaardigheden gaan we nu herhalen en specifiek toepassen binnen Unity.

### Basis Programmeervaardigheden in Unity (met C#)

#### 1. Basisprogrammeren in C#

- **Variabelen en datatypes**: Begrijpen en gebruiken van variabelen zoals `int` (getallen), `float` (decimale getallen), `string` (tekst), en `bool` (waar/niet waar) om informatie op te slaan (bijv. speler-score, snelheid).
- **If-statements**: Voorwaardelijke logica schrijven (bijv. `if (health <= 0) { Debug.Log("Game Over"); }`) voor beslissingen in de game.
- **Loops**: Werken met `for` en `while` loops om acties te herhalen (bijv. 5 keer een vijand spawnen).
- **Functies**: Zelf functies maken en aanroepen (bijv. `void Jump() { playerRb.AddForce(Vector3.up); }`) om code herbruikbaar te maken.
- **Collections (arrays, lists, dictionaries)**:
  - **Arrays**: Vaste lijsten maken en gebruiken (bijv. `int[] scores = new int[3] {10, 20, 30};` om scores op te slaan).
  - **Lists**: Dynamische lijsten beheren (bijv. `List<GameObject> enemies = new List<GameObject>(); enemies.Add(newEnemy);` voor een groeiende vijandenlijst).
  - **Dictionaries**: Sleutel-waarde paren gebruiken (bijv. `Dictionary<string, int> inventory = new Dictionary<string, int>(); inventory["coins"] = 50;` voor een inventaris).

#### 2. Unity-specifieke basisvaardigheden

- **MonoBehaviour begrijpen**: Weten hoe een script werkt met Unity’s basisclass (bijv. `Start()` voor eenmalige setup, `Update()` voor per-frame acties).
- **GameObjects manipuleren**: Objecten in de scène aanpassen via code (bijv. `gameObject.transform.position = new Vector3(0, 5, 0);` om iets te verplaatsen).
- **Componenten gebruiken**: Toegang krijgen tot componenten zoals `Rigidbody`, `Collider`, of `Animator` (bijv. `GetComponent<Rigidbody>()` om physics toe te passen).
- **Input verwerken**: Basisinput lezen (bijv. `if (Input.GetKeyDown(KeyCode.Space)) { Jump(); }`) voor spelerbesturing.

#### 3. Game Mechanics implementeren

- **Beweging**: Een object laten bewegen (bijv. `transform.Translate(Vector3.forward * speed * Time.deltaTime);` voor soepele beweging).
- **Collisions**: Botsingen detecteren met `OnCollisionEnter` of `OnTriggerEnter` (bijv. munt oppakken als de speler een trigger raakt).
- **Score en variabelen bijhouden**: Eenvoudige systemen maken (bijv. `int score; void OnTriggerEnter(Collider other) { score += 10; }`).
- **Timers**: Tijd bijhouden (bijv. `float timer = 60f; void Update() { timer -= Time.deltaTime; }`) voor levels of events.

#### 4. Samenwerking met Unity’s Editor

- **Public variabelen**: Waardes in de Inspector aanpasbaar maken (bijv. `public float speed = 5f;`) voor tuning zonder code te wijzigen.
- **Prefabs gebruiken**: Herbruikbare objecten instantiëren via code (bijv. `Instantiate(enemyPrefab, spawnPoint, Quaternion.identity);` voor vijanden).
- **Scenes beheren**: Basisnavigatie tussen scènes (bijv. `SceneManager.LoadScene("Level2");`) voor gameloops.

#### 5. Probleemoplossing en structuur

- **Foutmeldingen lezen**: Begrijpen van veelvoorkomende errors (bijv. "NullReferenceException") en deze oplossen.
- **Debuggen**: Fouten opsporen met `Debug.Log("Dit werkt");` om te zien wat er gebeurt in de game.
- **Code structureren**: Code netjes houden met comments (bijv. `// Speler springt`), en een logische indeling in functions (bijv. `private void Jump(float jumpForce){
//jump script}`).
- **Gegevensuitwisseling tussen scripts (script references)**: Informatie delen tussen scripts, bijvoorbeeld door een ander script te refereren (bijv. `public PlayerController player; void Start() { player.Jump(); }`) of via `GetComponent` (bijv. `GetComponent<ScoreManager>().AddScore(10);`) om mechanics te koppelen.

#### 6. Vector3 verdieping

- **Werking van een vector3 begrijpen**: Begrijpen hoe positionering en beweging in een 3d omgeving werkt.
- **Focus op de Lerp methode**: De studenten begrijpen wat de Lerp methode doet en hoe deze toe te passen is om een vloeiende beweging te maken.
- **Focus op Distance en Magnitude**: De studenten kennen deze 2 manieren om een afstand tussen 2 punten of de lengte van een vector op te meten. Ze kunnen dit toepassen.
- **Focus op Normalizen van een vector**: De studenten begrijpen wat normalizen is en dat het gebruikt kan worden in stappen van 1 met een vaste snelheid te kunnen bewegen.

#### 7. UI met TextMeshPro

Studenten leren hoe ze Unity’s UI met TextMeshPro gebruiken om informatie zoals score weer te geven. Na de les kunnen ze een score-UI updaten via code met `TMP_Text`.

#### 8. Coroutines

Studenten leren hoe ze `Coroutines` in Unity gebruiken voor tijdgebaseerde acties als alternatief voor `Update()`. Na de les kunnen ze een vijandspawn-systeem maken met vertragingen.

---
